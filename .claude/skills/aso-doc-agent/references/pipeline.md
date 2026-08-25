---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 0%

---
# ASO 문서 에이전트 — 파이프라인

`SKILL.md`에서 참조되었습니다. 이는 실행 순서에 대한 진실의 소스입니다. SKILL.md는
요약. 시작하기 전에 `config.yml`을(를) 읽습니다. 아래 `{braces}`의 모든 값은
구성 키.

**오류 처리(아래 단계마다 적용).** 오류가 발생하는 도구/API 호출(인증)
실패, 시간 초과, 잘못된 쿼리, 예기치 않은 스키마)는
합법적인 빈 결과이며,
&quot;empty&quot; 또는 &quot;nothing to do&quot; 분기(예: 1.2단계의 &quot;nothing to do here&quot;, 3.3단계)
&quot;서사시 백로그가 완전히 적용되었거나 모두 가동 중&quot;). 호출 오류 발생 시 을(를) 중지하고 기록하십시오.
깨끗하게 반환된 것처럼 계속 진행하는 대신 실행 요약에 실제 오류가 있습니다.

## 0단계 — Preflight

1. `pwd`과(와) 확인 `guidelines.md` + `.claude/skills/aso-doc-agent/config.yml`이(가) 모두 있습니다. 그렇지 않다면, 중지하십시오 — 잘못된 디렉토리.
2. `gh auth status` — `sandsinh_adobe` 계정에 이 호스트에 대한 올바른 토큰이 있는지 확인합니다. **실행 안 함`gh auth switch`** — 시스템 전체의 활성 `gh` 계정을 부작용으로 전환합니다. 이 계정은 무인 일일 실행을 위해 잘못된 계정으로 이 컴퓨터의 다른 터미널/프로세스를 자동으로 전환할 수 있습니다. 대신 이 실행의 범위를 `export GH_TOKEN=$(gh auth token --user sandsinh_adobe)`에서 시작할 때 한 번만 지정하므로, 아래의 모든 `gh` 호출은 전역 활성 계정에 관계없이 `GH_TOKEN` env var를 통해 해당 토큰을 사용합니다.
3. 누락된 경우 `mkdir -p {state_dir}`.
4. 존재하는 경우 `{state_dir}/run-state.json`을(를) 읽습니다(그렇지 않으면 `{"runs_completed": 0, "tracked_prs": []}`(으)로 처리됨). `tracked_prs`은(는) 열린 PR에 대한 이 에이전트의 고유 `{number, headRefName, key}` 목록입니다. `gh pr list --state open`만 삭제되면 PR을 볼 수 없으므로 병합하지 않고 닫은 PR(1.5단계)을 검색하는 데만 사용됩니다. 미디어 요청 타이밍은 별도의 파일에 있습니다. `{state_dir}/media-requests.json`(5단계) - GitHub와 Jira는 다른 모든 것(PR 상태, 티켓 상태)에 대한 신뢰할 수 있는 소스로 유지됩니다.
5. `--ticket KEY`이(가) 있음 -> 3단계의 자동 선택을 건너뛰고 KEY를 직접 사용합니다(여전히 4-7단계를 실행). 그렇지 않으면 3단계에서 자동으로 선택합니다.

## 1단계 — 이전 실행 조정

캡 게이트나 빈 실행에서도 이 작업을 항상 실행합니다.

1. `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json number,url,isDraft,headRefName,title,reviewDecision`
2. **검토 확인 — 열려 있는 모든 PR, 실행할 때마다**(`pr.check_reviews_every_run`):
   - `gh pr view <number> --repo {github.repo} --json reviewDecision,reviews,comments`
   - `reviewDecision == "APPROVED"` -> 지금 병합: `gh pr merge <number> --repo {github.repo} --merge`. 병합이 완료된 것으로 처리되기 전에 병합이 실제로 랜딩되었는지 확인합니다(`gh pr view <number> --json state,mergedAt` — `state == "MERGED"`). 보호된 분기 거부 또는 아직 보류 중인 필수 검사는 `gh pr merge`이(가) 호출된 후에도 PR을 열어 둘 수 있으며 병합된 것으로 Jira에 보고되지 않고 오류로 기록해야 합니다(시간 제한 기반 병합이 아닌 일반 사람이 승인한 병합). 병합이 확인된 경우: 병합한 연결된 Jira 티켓에 대한 댓글을 달면 `tracked_prs`에서 PR을 삭제합니다.
   - `reviewDecision == "CHANGES_REQUESTED"` -> 이 버전에서 PR을 **안 함** 자동 수정하지 않습니다. 리뷰 댓글(`gh api repos/{github.repo}/pulls/<number>/comments` 인라인 댓글과 `reviews` 필드의 최상위 리뷰 본문)을 읽고 아래의 **피드백에서 학습**&#x200B;을 실행하십시오. 실행 요약에 PR을 대기 중인 작성자 작업으로 기록합니다. 이 PR이 업데이트되지 않은 상태에서 `pr.stale_after_hours`보다 오래 `CHANGES_REQUESTED`인 경우 2단계 상한 게이트에 대해 오래된 것으로 플래그를 지정합니다. 이 PR은 사람에 대해 열려 있지만 더 이상 상한 슬롯을 차지하지 않습니다.
   - 기타 모든 작업(아직 리뷰가 없음, 리뷰가 제출되지 않은 `REVIEW_REQUIRED`) -> 여기서 수행할 작업이 없습니다.
3. **피드백을 통해 알아보기** 해당 PR과 관련된 일회성 수정 사항이 아닌 색조, 구조 또는 콘텐츠에 대해 *일반화 가능* 메모로 읽는 각 검토 주석 또는 검토 본문에 대해 &quot;항상 지원 무시를 사용하는 기회에 대해 무시된 탭 언급&quot;과 &quot;12행의 오타&quot;를 비교) - 날짜가 지정된 티켓 연결 항목을 `references/review-learnings.md`에 추가합니다. 단순히 기계적인 피드백(오타, 끊어진 링크, 보풀)을 건너뛰고 — PR 자체의 피드백을 수정하므로 지속적인 단원이 필요하지 않습니다. 정확한 항목 형식은 해당 파일에 설명되어 있습니다.
4. 해당 목록의 각 **초안** PR에 대해 분기 이름(`{github.branch_prefix}<KEY>-...`)에서 Jira 키를 추출하십시오.
   - 해당 키에 `mcp__Corp-Jira__list_attachments` + `mcp__Corp-Jira__get_jira_comments`이(가) 있습니다.
   - 요청된 캡처와 일치하는 새 이미지 첨부 파일 또는 `video.tv.adobe.com` URL이 포함된 댓글을 찾습니다.
   - 찾은 경우: `git fetch`/`checkout` 분기를 `help/**/assets/`에 이미지를 추가하거나(이미지 첨부 파일인 경우 `download_attachment`을 통해 다운로드) `>[!VIDEO](...)` 자리 표시자를 채우거나(비디오 URL 댓글인 경우) `experience-league-markdown`, 커밋, 푸시, `gh pr ready <number>`, PR &quot;Media added — review 준비됨&quot;에 대한 댓글을 확인하고 `{state_dir}/media-requests.json` 항목을 `resolved`(으)로 업데이트하십시오.
   - 찾을 수 없는 경우: `{state_dir}/media-requests.json`에서 요청 이후 경과 시간을 확인합니다. 5단계의 escalate/give-up 논리를 여기에 적용합니다(실행 간에 열려 있는 초안 PR에는 여전히 미디어를 추적해야 함) - 중단 경로의 `gh pr ready` 호출을 포함하면 중단 상태가 아닌 중단 상태의 초안을 계속 볼 수 있습니다.
5. **병합하지 않고 닫힌 PR 검색.** 이 실행의 열기 PR 목록(1단계)을 `run-state.json`의 `tracked_prs`과(와) 비교합니다. 열기 목록에서 누락된 모든 추적된 PR은 2단계에서 병합되지 않았으며 병합되지 않고 닫혔습니다. 이를 삭제하기 전에 최종 상태(`gh pr view <number> --repo {github.repo} --json reviews,comments`)를 가져와 마지막으로 **피드백에서 학습**&#x200B;을 한 번 실행하므로 사람의 거부 추론이 손실되지 않습니다. 그런 다음 추적에서 삭제합니다. 티켓 자체에 대한 추가 조치가 필요하지 않습니다. 청구 레이블은 게시 시간(6.10단계)에만 적용되므로 병합되지 않은 닫힌 티켓에는 이미 레이블이 없고 3.2단계 확인(열기/병합된 PR 없음)으로 인해 나중에 다시 선택할 수 있습니다.
6. `run-state.json`의 `tracked_prs`을(를) 현재 열기 PR 목록(`number`, `headRefName` 및 분기 이름에서 구문 분석된 Jira 키)으로 설정하여 다음 실행의 5단계를 비교 대상으로 지정합니다.

## 2단계 — PR 상한 게이트

1. 1단계의 `gh pr list` 출력에서 열려 있는 PR을 계산합니다. 단, 1.2단계에서 부실-`CHANGES_REQUESTED`(업데이트 없이 `pr.stale_after_hours`보다 오래 열림)로 플래그가 지정된 PR은 제외합니다. 이러한 PR은 사람에 대해 열려 있지만 더 이상 캡 슬롯을 차지하지 않습니다.
2. count >= `{pr.max_open}` (3): 로그 `"cap reached ({count}/{pr.max_open} open) — skipping new ticket this run"`인 경우 7단계로 이동하십시오.
3. 3단계로 진행합니다.

## 3단계 — 티켓 선택

`--ticket KEY`이(가) 전달된 경우 완전히 건너뜁니다(키 사용).

```
JQL: "Epic Link" = {jira.epic} AND status = "{jira.open_status}"
     ORDER BY priority DESC, created ASC
```

1. 검색(`mcp__Corp-Jira__search_jira_issues`, `minimizeOutput: true`, `key,summary,priority,status,labels`(으)로 제한된 필드)을 실행합니다.
2. 순서대로 결과 이동 다음과 같은 티켓 건너뛰기:
   - 이미 `{jira.picked_label}` 레이블이 있거나
   - 원격(`git ls-remote --heads origin '{github.branch_prefix}<KEY>-*'`)에 이미 `{github.branch_prefix}<KEY>-*` 분기가 있습니다. 또는
   - 이미 열려 있거나 병합된 PR이 있습니다(1단계의 목록/`gh pr list --state all --search <KEY>`에 대해 상호 확인).
3. 세 가지 검사를 모두 통과하는 첫 번째 티켓이 선택입니다. 검색에서 실제로 0개의 적격 티켓이 반환되었으므로 **을(를) 통과하지 못한 경우**&#x200B;을(를) `"epic backlog fully covered or all in flight"`에 로그하여 7단계로 이동하십시오. 검색 자체가 실패한 경우(인증 오류, 시간 초과, 잘못된 JQL), 이 경우가 아니면 대신 실제 오류를 기록합니다(위의 오류 처리 참조).
4. 아직 티켓에 레이블을 **not**(으)로 지정하지 마십시오. 클레임 레이블은 분기 및 PR이 실제로 존재하는 경우에만 6.10단계에서 적용됩니다. 4-5단계(연구/초안/미디어)는 티켓에 아무 흔적도 남기지 않고 실패하거나 충돌할 수 있습니다. 6단계 전에 진행 중인 유일한 신호는 위의 분기 존재/사전 존재 확인이며, 이는 실제 동시성이 없는 단일 시스템에서 실행되므로 충분합니다.

## 4단계 — 연구 + 초안

조사가 먼저 시작되며 **다중 소스**&#x200B;입니다. 단 하나의 입력에서 초안을 작성하지 않습니다(Jira).
티켓만 사용할 수도 있고 형제 문서를 읽을 수도 있습니다). 아래의 모든 소스는 또는
다른 문제를 해결합니다. 소스 코드 > Wiki/PR 문서 >
Slack 토론 > 문서 작성자 자신의 추론을 해당 순서로 나열하고 인라인 플래그를 지정합니다
해결할 수 없는 경우 `<!-- CONFIRM -->`(으)로 설정합니다.

&#x200B;0. **리뷰 레슨을 누적했습니다.** 먼저 `references/review-learnings.md`을(를) 읽습니다. 초안을 작성하기 전에 이 티켓의 주제와 관련이 있는 것은 무엇이든 적용하십시오. 즉, 과거 PR 검토의 피드백이 동일한 수정을 반복하는 대신 향후 초안을 개선하는 방법입니다.

### 연구(모든 항목 적용 - 바로 초안으로 건너뛰지 않음)

1. **Source 코드(실제 작동 방식에 대한 기본 정보).** 기본 UI 저장소(`research.code_repos` in config.yml)에서 기능의 어댑터/핸들러(`*OpportunityAdapter.tsx`, `*SuggestionAdapter.tsx`), 해당 데이터 후크(`use*Data.ts`) 및 해당 `.l10n.ts`/`.I10n.ts` 제목/설명 문자열을 검색합니다. 이는 필드 이름, 데이터 모양, 범주 및 정확한 제품 사본에 대한 권한입니다. 출처가 동의하지 않으면 다른 어떤 것보다도 선호합니다.
2. **Wiki(디자인 의도, 사양, 의사 결정).** 기능/영업 기회 이름과 서사시/티켓 키가 있는 `mcp__Adobe-Wiki__search_wiki_content`. 일치하는 페이지(`get_wiki_content`) 읽기: 기능이 존재하는 이유, 제품 팀이 사용하는 용어, 문서화된 UX 흐름 또는 극단적 사례, 실제 UI의 모양을 설정하는 포함된 스크린샷(5단계에서 미디어 캡처 사양에 알리고 페이지가 최신 상태가 아닌 경우 실제 새 스크린샷을 대체하지 않음).
3. **Slack(팀에서 실제로 어떻게 이야기하고 있는지, 열려 있는 질문, 최근 변경 사항).** `research.slack_channels`이(가) config.yml에서 범위를 좁히지 않는 한 채널에 의해 제한되지 않은 기능/기회 이름과 티켓 키를 가진 `mcp__Slack__slack_search_messages`입니다. 찾기: 공지 메시지(종종 깔끔한 고객 대면 프레이밍이 있음), 디자인 토론 스레드, 형제 문서 또는 코드 주석이 아직 반영되지 않은 방식으로 최근에 변경된 기능을 나타내는 모든 것을 표시합니다.
4. **GitHub PR 기록(구현 이유, 스크린샷, 토론 검토).** `research.code_repos`의 `gh search prs --repo <repo> "<feature name>"` 또는 `gh pr list --repo <repo> --search "<ticket key OR feature name>" --state all`. 코드만으로는 설명하지 않는 비헤이비어(예: 수정 유형이 제어되는 이유, UI에서 극단적 사례가 표시되는 방식)를 명확하게 하는 근거, 연결된 디자인 문서 및 스크린샷에 대한 병합된 PR 설명을 읽으십시오.
5. **톤 유사체** 티켓 요약을 기반으로 2~3개의 가장 가까운 기존 페이지를 찾습니다.
   - &quot;... 영업 기회 방법&quot; 티켓 -> `help/documentation/opportunities/`에 있는 2개의 형제 파일 읽기(실제 영업 기회당 방법 위치 — `help/opportunity-types/*.md`은(는) 사용 방법 콘텐츠 자체가 아니라 여기에 연결된 카드 그리드가 있는 범주 랜딩 페이지임).
   - 설정/워크플로/연결 티켓 -> `help/documentation/`에서 1-2 형제 파일을 읽습니다(`setup/`, `opportunities/`, `settings.md`, `basics.md`에서 가장 가까운 일치 항목 확인).
     미러 제목 구조, 메모 상자 사용, 문장 길이, 기술적 세부 사항 수준.
6. **규칙 서식** 쓰기 전에 `experience-league-markdown` 스킬의 빠른 참조를 다시 읽으십시오. 모든 제목/메모/이미지/링크는 구문과 정확히 일치해야 합니다.

### 초안

&#x200B;7. **대상 파일 결정** 티켓이 기존 독립 실행형 페이지의 세부기간과 일치하지 않는 한 새 파일을 만드는 것보다 기존 페이지의 관련 섹션을 확장하는 것이 좋습니다(예: 각 영업 기회는 `help/documentation/opportunities/` 아래에 자체 파일을 얻음 - 새 영업 기회는 기존 형제 페이지의 정확한 구조를 따름). 기존 페이지를 확장할 때 이 티켓의 한 섹션만 터치하십시오. 오래된 섹션이라도 관련 없는 섹션은 편집하지 마십시오. 새 독립 실행형 페이지의 경우 관련 `help/opportunity-types/*.md` 랜딩 페이지(기존 카드의 정확한 패턴과 일치하는 소스 댓글 목록 + 생성된 HTML 블록)에도 해당 카드를 추가하고 `help/main-toc/TOC.md`에 등록합니다.
&#x200B;8. **초안 v1.** 지금 컨텐츠 작성(저장소 파일에 아직 없는 메모리/스크래치) - 미디어 결정 후 6단계에서 발생하므로 미디어 보류 문서와 미디어 해결 문서는 동일한 쓰기 경로를 거칩니다. 모든 단계 1-6 을 합성 — 그냥 Jira 티켓 설명을 다시 기술하지 마십시오.
&#x200B;9. **반복.** 1-4단계의 모든 연구 결과에 대해 v1 초안을 다시 읽으십시오. 초안이 Slack 또는 Wiki가 표시된 것을 놓쳤습니까? 소스 코드가 실제로 수행하는 작업과 모순됩니까? 형제자매 어투와 최대한 가깝게 어울리나요? 계속하기 전에 수정하십시오. 이것은 형식적이 아니라 실제 두 번째 패스입니다. 이 패스(4개의 소스 중 어느 것에서도 찾을 수 없음) 이후에 실제로 확인되지 않은 모든 내용이 추측이 아닌 인라인 `<!-- CONFIRM -->` 댓글을 받습니다.
&#x200B;10. **미디어 결정** `mediaNeeded: true|false`을(를) 결정합니다.
    - `true` 기능이 텍스트 설명만 따르기 어려운 다단계 UI 워크플로우인 경우(텍스트 설명이 부족한 경우 `guidelines.md`의 &quot;신중하게 사용됨...&quot;과 일치).
    - `true`인 경우 다음을 생성합니다. `mediaType`(`screenshot` 또는 `video`), `captureSteps`(캡처할 상태를 재현하는 정확한 단계), `urls`(고객 응대 앱 URL 및/또는 해당 상태에 도달하기 위해 필요한 내부 페이지 URL — Jira 티켓 설명/주석, Wiki 또는 `open-aso-devmode-url` 규칙에서 참조되는 경우 실제 URL을 가져옵니다. URL을 만들지 않음).
    - `false`이면 이 티켓의 5단계를 건너뜁니다.

## 5단계 — 미디어 게이트

4단계에서 `mediaNeeded: true`을(를) 설정한 경우에만 실행됩니다. 의 모든 타임스탬프
`{state_dir}/media-requests.json`은(는) UTC ISO-8601(`date -u +%Y-%m-%dT%H:%M:%SZ`)입니다.
항상 이 형식으로 작성하고 비교하므로 아래 경과 시간 수학이 명확합니다.
를 클릭합니다.

1. 이 티켓 키의 기존 항목을 `{state_dir}/media-requests.json`에서 확인하십시오. 없는 경우 새로 요청한 것입니다.
2. **새 요청:**
   - `media.contacts_in_order[0].email`(샌드박스)의 `mcp__Slack__slack_lookup_user`에서 Slack 사용자 ID를 가져옵니다.
   - `mcp__Slack__slack_send_dm` 메시지에 Jira 티켓 키 + 링크, 캡처할 항목(`captureSteps`), 사용할 URL 및 답변이 표시되는 위치(&quot;Jira 티켓에 회신 — 스크린샷을 직접 첨부하거나 비디오의 경우 일반적인 Experience League 비디오 양식을 통해 업로드하고 결과 `video.tv.adobe.com` 링크를 댓글로 붙여넣기&quot;)가 포함되어 있습니다.
   - `{state_dir}/media-requests.json[KEY] = {requestedTo: "sandsinh", requestedAt: <UTC ISO-8601 now>, escalated: false}`을(를) 씁니다.
3. **기존 요청:** 아래 두 임계값은 원래 `requestedAt`에서 측정됩니다. 확대해도 시계가 재설정되지 않습니다.
   - `now - requestedAt` &lt; `media.escalate_after_hours` -> 이 작업을 실행하지 않고 아직 보류 중인 미디어를 사용하여 게시로 진행합니다(초안 PR).
   - `now - requestedAt` >= `media.escalate_after_hours`, 아직 에스컬레이션되지 않음 -> DM `media.contacts_in_order[1]`(kanishka), 메시지 메모 샌드싱이 응답 없이 N시간 전에 이미 요청되었습니다. 항목 업데이트: `escalated: true, escalatedAt: <UTC ISO-8601 now>`.
   - `now - requestedAt` >= `media.give_up_after_hours`(에스컬레이션 상태 무관) -> 게시 목적으로 `mediaNeeded: false`을(를) 설정합니다. 초안에 인라인 메모를 삽입합니다. `>[!TIP]\n>\n>A screenshot for this step is being added in a follow-up update.` 이 티켓에 대한 PR이 이미 있고 아직 초안인 경우(6단계 게시가 아닌 1.4단계를 통해 여기에 도달함), `git fetch`/분기를 체크아웃하고, 메모를 적용하고, 커밋하고, 푸시하고, `gh pr ready <number>`(). 지정된 초안을 계속 볼 수 있어야 하며 무기한 중단되지 않아야 합니다. `gaveUp: true` 항목을 표시합니다.

## 6단계 — 게시

3단계에서 티켓을 완전히 건너뛰면 건너뜁니다(게시할 내용이 없음).

1. `git fetch origin` 및 `git checkout -B {github.branch_prefix}<KEY>-<short-slug> origin/main` — `-B`(`-b`이(가) 아님). 따라서 충돌한 이전 실행에서 남은 로컬 분기가 체크아웃을 차단하지 않고 재설정됩니다. `origin/main`에서 직접 분기하면 충돌한 이전 충돌에서 더러운 로컬 상태도 실패하지 않고 삭제됩니다.
2. 4.3단계에서 결정된 대상 파일에 4단계 초안을 작성합니다. `experience-league-markdown`의 &quot;Markdown 변경 내용을 커밋하기 전&quot; 체크리스트를 줄별로 다시 확인합니다.
3. Markdown 링크가 구성되어 있고(`markdownlint_custom.json` 저장소 루트에 있음) `markdownlint-cli`/`npx markdownlint`을(를) 사용할 수 있는 경우 변경된 파일에 대해 실행하고 커밋하기 전에 위반을 수정하십시오.
4. 커밋: `docs(aso): <ticket summary, lowercase, no trailing period>\n\nSITES-XXXXX`.
5. `git push -u origin <branch>`.
6. 검토자 선택: `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json reviewRequests` — 구성된 두 검토자를 각각 나열하는 현재 수를 계산합니다. 둘 중 더 적은 항목을 할당합니다(-> `sandsinh_adobe` 연결).
7. PR 본문:

   ```
   ## Summary
   [1-2 sentence description of the feature now documented]
   
   ## Source
   Closes documentation gap tracked in [SITES-XXXXX](https://jira.corp.adobe.com/browse/SITES-XXXXX)
   
   ## Media
   [either "No media needed for this update." OR "Screenshot/video requested from {contact} on {date} — PR opened as draft until resolved." OR "Media follow-up pending — shipped without it; see inline note."]
   
   > 🤖 Drafted by aso-doc-agent
   ```

8. 미디어가 아직 보류 중인 경우 `gh pr create --repo {github.repo} --title "<ticket summary>" --body "<above>" --label {github.pr_label} --reviewer <chosen-github-handle> --draft`을(를) 제외하고 `--draft`을(를) 생략합니다.
9. 레이블 플래그를 지정하지 않은 경우 `gh pr edit <number> --add-label {github.pr_label}`(벨트 및 일시 중단기, 이 조직의 도구 설명에 사용된 패턴과 일치)
10. Jira: `add_jira_comment`이(가) PR URL을 연결하고 이제 이 실행에서 처음으로 `{jira.picked_label}`을(를) 추가합니다(`update_jira_issue`, 기존 레이블과 병합). 이는 의도적으로 한 지점과 PR이 모두 존재하는 경우에만 적용되는 주장입니다. 3-5단계의 어느 곳에서든 충돌이 발생하면 티켓이 영구적으로 고정된 대신 레이블이 완전히 지정되지 않고 안전하게 다시 선택할 수 있습니다. 티켓 상태를 전환하지 않음 — 문서 팀의 자체 분류에 그대로 둡니다. `{jira.picked_label}`은(는) 이 에이전트가 작성하는 유일한 상태 신호입니다.

## 7단계 — 요약 실행

1. `{state_dir}/run-state.json` 업데이트: `runs_completed += 1`, 타임스탬프, 선택된 티켓(또는 &quot;없음&quot; + 이유), PR 열림/업데이트됨(또는 &quot;없음&quot; + 이유), 상한 상태.
2. 사람이 읽을 수 있는 짧은 요약(티켓, 수행한 작업, PR 링크, 미디어 상태)을 인쇄합니다.
