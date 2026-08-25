---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---
# ASO 문서 에이전트 — 사용

이것이 무엇이며, 어떻게 실행되며, 필요할 때 어떻게 해야 합니까?

## 설명

이 에이전트는 매일 다음 중에서 우선 순위가 가장 높은 문서화되지 않은 ASO 기능을 선택합니다.
[SITES-49539](https://jira.corp.adobe.com/browse/SITES-49539)의 백로그(예: 39개 티켓)
&quot;정식 영업 기회 방법&quot;, &quot;Slack 알림&quot;)은 문서 한 개를 작성합니다
이 보고서의 하우스 스타일에 대해 설명하고 PR을 엽니다. 둘 중 하나를 지정합니다.
구성된 검토자(`sandsinh_adobe`/`kanishka_adobe`)의 현재 열기 횟수가 더 적습니다.
이 에이전트의 요청을 검토합니다. 기능에 스크린샷이나 비디오가 필요한 경우
PR을 완료하기 전에 Slack에서 한 번.

모든 실행 시 모든 진행 중인 PR의 검토 상태도 확인합니다. 승인된 PR이 병합됩니다.
즉시 변경 요청 피드백이 읽히고 일반화할 수 있는 경우
레슨 (일회성 오타가 아님), 나중에 초안이 같은 실수를 반복하지 않도록 기록됩니다.

한 번 실행 = 한 개 기능 = 최대 한 개의 PR. 한 번에 한 장씩 건드리는 건 아니지만,
한 번에 3개 이상의 PR을 열지 않습니다(기존 PR이 먼저 병합/닫힐 때까지 대기).

## 모든 것이 존재하는 곳

| 내용 | 경로 |
|---|---|
| 어떻게 할지 결정하는 방법 | `.claude/skills/aso-doc-agent/SKILL.md` |
| 정확한 단계별 방법 | `.claude/skills/aso-doc-agent/references/pipeline.md` |
| 팀별 설정(검토자, 상한, 에스컬레이션 시간을 변경하려면 이 설정을 편집) | `.claude/skills/aso-doc-agent/config.yml` |
| PR 검토 피드백에서 얻은 교훈(git에서 추적되고, 모든 초안 전에 읽음) | `.claude/skills/aso-doc-agent/references/review-learnings.md` |
| 로컬 실행 상태(gignored — 삭제해도 안전하며 재구축됨) | `.claude/skills/aso-doc-agent/state/` |
| 일별 예약 설치 관리자 | `.claude/scripts/aso-doc-agent-setup.sh` |
| 헤드리스 실행 허용 | `.claude/settings.local.json`(gignored, machine-local) |

## 실행 중

- **일반 세션에서 수동으로:** `/aso-doc-agent`(또는 `/aso-doc-agent --ticket SITES-XXXXX`)
- 저장소 루트에서 **헤드리스, 일회성:** `claude -p "/aso-doc-agent"`
- **일별, 무인:**&#x200B;이(가) `launchctl`을(를) 통해 이미 설치되었습니다(아래 참조). 매일 현지 시간으로 07:53에 실행되며 조치가 필요하지 않습니다.

### 일별 일정 설치/변경

```bash
bash .claude/scripts/aso-doc-agent-setup.sh
```

다음과 같은 `launchd` 작업(`~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist`)을 설치합니다.
이 리포지토리에서 매일 `claude -p "/aso-doc-agent"`을(를) 실행합니다. 언제든지 스크립트 재실행
내에서 일정을 편집합니다(기본값: 07:53 로컬). 이 기능은 시스템이 작동하는 동안에만 작동합니다.
해당 시간에 실행 및 절전 모드 해제 - launchd는 누락된 작업을 소급하여 실행하지 않지만 실행됩니다.
일반적으로 다음 예약된 시간.

```bash
launchctl list | grep com.sandsinh.aso-doc-agent   # confirm it's loaded
launchctl start com.sandsinh.aso-doc-agent         # trigger a run right now, don't wait for 07:53
launchctl unload ~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist  # stop it
```

의 각 예약된 실행 랜드에서 로그 `.claude/skills/aso-doc-agent/state/launchd.out.log`
및 `launchd.err.log`.

## 요청 사항

- **에이전트의 Slack DM**(귀하로 전송) — sandsinh first, kanishka on
(에스컬레이션) 스크린샷 또는 비디오에 정확한 캡처 단계 및 URL 요청
를 사용하십시오. **Slack이 아닌 연결된 Jira 티켓에 회신**: 스크린샷을 직접 첨부하고,
또는 비디오의 경우 일반적인 Experience League 비디오 양식을 통해 업로드하십시오
(`experience-league-video-upload` 스킬) 결과 붙여넣기 `video.tv.adobe.com`
jira 주석으로 링크. 다음 실행에서 자동으로 선택됩니다.
- **5일** 내에 아무도 응답하지 않으면 요청이 샌드싱에서 카니슈카로 에스컬레이션됩니다
자동으로 표시됩니다. **10일** 후 어느 쪽에서도 응답이 없으면 에이전트가 문서를 보냅니다
미디어 없이 인라인 메모를 추가합니다. 시간 초과 기반 자동 병합 — PR
그러나 시간이 오래 걸리더라도 실제 인류의 검토를 기다립니다.
- **검토할 PR** — 두 사람 중 에이전트에서 연 PR이 적은 사람에게 할당됩니다.
현재 검토 대기 중입니다. PR 초안은 미디어가 아직 보류 중임을 의미합니다.
에셋이 표시되면 자동으로 검토 준비됨. 승인하면 에이전트가 병합됩니다.
다음 실행 시 — 별도의 병합 단계가 필요하지 않습니다.
- **변경을 요청하면** 에이전트가 다음 실행 시 댓글을 읽습니다. 일반화 가능
(오타/링크 수정 아님) 피드백이 `references/review-learnings.md`에 기록되므로
향후 PR에서 동일한 수정을 반복할 필요가 없습니다.

## 동작 조정

`.claude/skills/aso-doc-agent/config.yml` 편집(git에서 추적됨) - 변경 사항은 모든 항목에 영향을 미칩니다.
이 컴퓨터 또는 저장소를 복제하는 다른 사용자의 향후 실행:

- `pr.max_open` — 에이전트가 새 티켓 선택을 일시 중지하기 전에 열려 있는 PR 수(기본값 3)
- `pr.stale_after_hours` — `CHANGES_REQUESTED` PR이 `pr.max_open`(기본값 336 = 14일) 쪽으로 카운트되는 것을 중지하기 전에 대기할 수 있는 시간입니다. 열려 있는 동안에는 새 선택만 차단됩니다
- `github.reviewers` — 할당 대상과 균형
- `media.contacts_in_order` / `escalate_after_hours`(기본값 120 = 5일) / `give_up_after_hours`(기본값 240 = 10일) — 질문한 사람, 순서 및 인내심을 묻는 사람. 둘 다 원래 요청에서 측정되므로 에스컬레이팅이 중단 날짜를 밀어내지 않습니다.
- `pr.check_reviews_every_run` — 검토 확인 단계를 끕니다(권장하지 않음. 병합 및 학습 수행 방식).

## 권한 프롬프트에서 중단되는 경우

Headless(`claude -p`, launchd) 실행에는 목록에 없는 도구 호출 메시지를 표시할 터미널이 없습니다.
실패하는 것보다는 실패하는 것입니다. 실행 로그에 명령에 대한 권한 거부가 표시되는 경우
파이프라인이 필요한 경우 `permissions.allow` 목록에 추가합니다.
`.claude/settings.local.json`(git에서 추적되지 않음 — 시스템-로컬; 모든 개발자가 실행 중
이 에이전트에게는 자체 scoped 허용 목록이 필요합니다.

## 진전을 완전히 멈추면

다음 순서로 확인합니다.
1. `gh pr list --repo Adobe-Enterprise-Docs/experience-manager-sites-optimizer.en --label aso-doc-agent --state open` — 3개가 표시되면 중단 없이 검토 대기 중입니다.
2. Jira: SITES-49539 아래에 아직 `aso-doc-agent-picked`이(가) 아닌 자격 있는 `New` 티켓이 남아 있습니까? 레이블은 분기+PR이 존재하는 경우에만 적용됩니다(pipeline.md Step 6.10). 따라서 충돌한 실행은 레이블이 있지만 게시되지 않은 티켓을 남겨서는 안 됩니다. 아직 티켓(예: 수동으로 추가된 레이블)이 있는 경우 수동으로 제거하여 티켓을 다시 사용할 수 있도록 하십시오.
3. `.claude/skills/aso-doc-agent/state/launchd.err.log`(가장 최근 실행 오류).
4. 실행의 요약에 &quot;서사시 백로그가 완전히 덮였다&quot; 또는 &quot;여기서 할 일 없음&quot;이 표시되지만 적합한 작업이 있어야 한다는 것을 알고 있다면 이를 의심스러운 것으로 처리하십시오. 해당 메시지는 완전히 빈 결과를 위해 예약되어 있습니다. 실제 Jira/GitHub/Slack 오류는 별도로 기록되며, 이러한 메시지 중 하나 뒤에 숨지 않고 `launchd.err.log`에 고유한 줄로 표시되어야 합니다.
