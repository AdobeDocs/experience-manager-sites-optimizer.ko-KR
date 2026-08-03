---
description: 내부 ASO 스프린트 릴리스 노트를 고객 대면 Experience League 형식으로 변환하고 릴리스 노트 페이지에 추가합니다.
source-git-commit: 5f400c37283d1a3d8285b4d2ac5246761a7275e6
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# 릴리스 노트 변환기

Slack `#aem-sites-optimizer-announcements` 채널 또는 `.cursor/commands/release-notes` 커서 출력의 내부 sprint 릴리스 정보를 고객 응대 항목으로 변환하여 `help/documentation/release-notes.md`에 추가합니다.

## 사용량

이 스킬을 호출한 다음 메시지가 표시되면 내부 릴리스 노트 콘텐츠를 붙여넣습니다. 이 스킬은 다음과 같은 작업을 수행합니다.

1. 필터링 및 톤 규칙에 대해 아래 지침을 적용하십시오.
2. 내부 릴리스 정보를 구문 분석합니다(이모지로 분류된 섹션: ✨ 기능, 🚀 개선 사항, 🤖 AI 우선, 🔧 수정 사항, 🏢 BackOffice).
3. 지침별로 제외된 모든 카테고리를 필터링합니다(AI 도구, 백오피스, 로컬라이제이션 린터, E2E 테스트, 사이트내부 전용 항목).
4. 아래 톤 예제를 참조로 사용하여 나머지 항목을 고객 응대 톤으로 다시 작성합니다.
5. 관련 항목을 역량 영역별로 그룹화합니다(팀이나 리포지토리별로 그룹화하지 않음).
6. 아래 페이지 구조 템플릿 다음에 오는 새 릴리스 항목으로 형식을 지정하십시오.
7. 새 항목 앞에 `help/documentation/release-notes.md`을(를) 추가합니다(이전 최신 항목 위, 페이지 소개 단락 아래).
8. 항목 보관, 재작성, 항목 삭제(각 항목 삭제 사유 포함)를 보여 주는 요약 테이블을 인쇄합니다.

## 지침

### 핵심 원칙

1. **고객 혜택 먼저.** 모든 항목에서 &quot;이전에는 할 수 없었던 지금 무엇을 할 수 있습니까, 아니면 더 잘할 수 있습니까?&quot;라고 답해야 합니다. &quot;무엇을 선적했는가?&quot;가 아닙니다. 구현이 아닌 값으로 영업을 전개하십시오.

2. **리더십 색조** 의사 결정자를 위해 작성하십시오. 기술 역학이 아닌 결과와 능력입니다. Digital Experience의 VP는 업데이트가 중요한 이유를 즉시 이해해야 합니다.

3. **내부 전문 용어가 없습니다.** 모든 팀 내부 축약 바꾸기:
   - &quot;PLG&quot; → &quot;평가판 사용자&quot; 또는 &quot;신규 고객&quot;
   - &quot;BackOffice&quot; →은 완전히 생략됩니다(인프라 전용 변경).
   - &quot;MSM&quot; → &quot;AEM 다중 사이트 관리자&quot;
   - &quot;SHM&quot; → &quot;Site Health Monitor&quot;
   - &quot;OrcaFix&quot;, &quot;Cursor commands&quot;, &quot;AGENTS.md&quot; → 완전히 생략됨
   - &quot;EDS&quot; → &quot;Edge Delivery Services&quot;

4. **짧은 항목** *내용*&#x200B;의 한 문장, *중요한 이유*&#x200B;의 한 문장. 둘 다 한 문장에 맞으면 그렇게 하세요.

5. **정확한 범위** 고객이 제품 UI에서 보게 되거나 워크플로우에서 경험하게 되는 변경 사항만 포함합니다. 인프라, 도구 및 개발자 경험 변경 사항은 제외됩니다.

6. **조기 액세스 기능에 플래그를 지정합니다.** 기능이 기본적으로 꺼져 있는 기능 플래그 뒤에 제공되는 경우(예: LaunchDarkly `FeatureGate`/`isEnabledByDefault={false}`을(를) 통해 조직/사이트당 옵트인) 굵은 기능 이름에 `(Early Access)`을(를) 추가하십시오. 이 경우 눈금 기능에 사용되는 기존 `(General Availability)` 규칙을 미러링합니다. 확실하지 않은 경우 모든 고객에 대해 기능이 기본적으로 켜져 있는지 확인하고 그렇지 않은 경우 조기 액세스입니다. 코드에서 기능 플래그가 기본적으로 지정되어 있는지 확인합니다. — 추측하지 마십시오.

### 페이지 구조 템플릿

각 릴리스 항목은 다음 구조를 따릅니다.

```markdown
## [Month Start]–[Day End], [Year]

### New Features

- **[Feature Name]** — [One-sentence benefit statement. One sentence of business context if needed.] (append `(Early Access)` or `(General Availability)` to the feature name when the feature's availability status is notable)

### Enhancements

- **[Enhancement Name]** — [One-sentence improvement statement.]

### Bug Fixes

- [Short description of what was fixed and why it matters to users.]
```

**규칙:**
- 날짜 범위 형식: `May 11–22, 2026`(en-dash, 약식 월, 4자리 연도).
- 역시간 순서: 페이지 상단에 있는 최신 릴리스.
- 콘텐츠가 있는 섹션만 포함합니다. 비어 있는 경우 &quot;개선 사항&quot; 또는 &quot;버그 수정&quot;을 생략합니다.
- 버그 수정 항목은 굵은 기능 이름을 사용하지 않습니다. 일반 글머리 기호입니다.
- 사용자가 볼 수 있는 수정 사항 중 주목할 필요가 있는 것이 3개 이상인 경우에만 버그 수정 사항을 포함합니다.

### 포함 및 제외 대상

**포함:**

| 범주 | 예 |
|---|---|
| 새로운 영업 기회 유형 | 광고 의도가 일치하지 않습니다. 접힌 부분 위에 CTA이 없습니다. |
| 새로운 보기 또는 워크플로 | 배포된 탭, CSV 내보내기, Jira 연결 |
| 평가판/온보딩 개선 사항 | 안내가 있는 설정 흐름, 사이트 온보딩된 상태가 없음 |
| 설정 개선 사항 | 감사 대상 URL, 전달 유형 구성 |
| 의미 있는 UX 수정 사항 | 잘못된 카운트, 탐색 중단, 결정에 영향을 주는 표시 문제 |
| 새로운 데이터/통합 | 유기 검색의 데이터 준수, 보안의 종속성 트리 |
| 작성자 배포 기능 | 직접 배포를 지원하는 새로운 영업 기회 유형 |

**제외:**

| 범주 | 이유 |
|---|---|
| AI 도구(OrcaFix, Cursor 명령, AGENTS.md, Cloud Code 규칙) | 내부 개발자 도구, 고객이 볼 수 없음 |
| 로컬라이제이션 린터/사전 커밋 후크 | 제품 기능이 아닌 엔지니어링 프로세스 |
| 백오피스 / 인프라 변경 | 최종 사용자 행동을 변경하지 않는 한 UI에 표시되지 않음 |
| React Spectrum 버전 업그레이드 | 내부 종속성, 사용자에게 표시되지 않음 |
| E2E 테스트 개선 사항 | 제품 기능이 아닌 엔지니어링 품질 |
| 릴리스 파이프라인 자동화 | 내부 프로세스 |
| SitesInternal 전용 기능 | 고객이 사용할 수 없음 |

### 톤 예

| 내부 구문 | 고객용 구문 |
|---|---|
| &quot;수동 유효성 검사 워크플로우에 대해 거부됨 상태가 도입됨&quot; | &quot;이제 제안을 거부됨으로 표시하여 사이트에 적용되지 않음을 나타낼 수 있으며, 영업 기회 목록을 실행 가능한 항목에 중점을 둘 수 있습니다.&quot; |
| &quot;Canonical 및 Hreflang 기회에 대해 배포된 보기(날짜별로 그룹화)&quot; | &quot;이제 Canonical 및 Hreflang 기회에 대한 변경 사항이 배포됨 탭에서 배포 날짜별로 그룹화되어 수정된 항목과 시기에 대한 명확한 기록을 제공합니다.&quot; |
| &quot;Alt Text Autofix V2 — &#39;수정 가능성 확인&#39; 사전 평가&quot; | &quot;대체 텍스트 수정 사항을 배포하기 전에 실행 전 검사를 실행하여 수정 사항이 콘텐츠에 성공적으로 적용되었는지 확인할 수 있습니다.&quot; |
| &quot;SHM 지표에 대한 96% 스토리지 최적화&quot; | 생략 — 인프라만 |
| &quot;공식 에이전트 역할 및 안전 보호 기능이 있는 AGENTS.md&quot; | 생략 — 내부 AI 도구 |
| &quot;E2E 테스트 성능 최적화(~6분 →~5분)&quot; | 생략 — 엔지니어링 프로세스 |

### 그룹화 규칙

- 팀이나 리포지토리가 아닌 기능 영역별로 **그룹화**&#x200B;합니다. 예를 들어, 모든 대체 텍스트 개선 사항(기능, 개선 사항 및 수정 사항)은 동일한 영역에 속합니다. 이러한 개선 사항을 섹션 간에 분산하지 마십시오.
- **밀접하게 관련된 수정 사항을 각각 나열하지 않고 하나의 글머리 기호로 통합**&#x200B;합니다(예: &quot;유료 트래픽, 접근성 및 보안 기회에서 여러 디스플레이 및 레이아웃 개선&quot;).
- **버그 수정 임계값 섹션**: 호출할 수 있는 사용자 표시 수정 사항이 3개 이상 있는 경우에만 이 섹션을 포함합니다. 이 임계값 아래의 사소한 수정 또는 단순한 외관 수정은 생략해야 합니다.

## 단계

1. 이 파일의 지침 적용 — 모든 원칙, 포함/제외 규칙, 톤 예제 및 그룹화 규칙을 내부화합니다.
2. 아직 제공되지 않은 경우 적용 날짜 범위(예: &quot;2026년 5월 11~22일&quot;)를 사용자에게 요청합니다.
3. 사용자에게 내부 릴리스 노트 콘텐츠를 붙여넣거나 파일 경로를 수락하도록 요청합니다.
4. 콘텐츠를 처리합니다.
   - 각 섹션(✨/🚀/🤖/🔧/🏢) 및 글머리 기호를 **구문 분석**&#x200B;합니다.
   - 위의 Exclude 테이블당 **필터**. 드롭된 각 항목에 이유를 표시합니다.
   - **다시 작성**&#x200B;이(가) 항목을 고객 색조로 유지합니다. 이점 우선, 전문 용어 없음, 짧은 항목.
   - 여러 항목이 관련된 기능 영역별 **그룹**
   - **임계값 확인**: 사용자가 볼 수 있는 수정 사항이 3개 이상인 경우 &quot;버그 수정&quot; 섹션만 포함하십시오.
5. 위의 페이지 구조 템플릿을 사용하여 새 항목의 형식을 지정합니다.
6. `help/documentation/release-notes.md`의 현재 콘텐츠를 읽습니다.
7. 페이지 소개 단락 바로 뒤(이전 최신 `##` 날짜 제목 앞)에 새 항목을 삽입합니다.
8. 업데이트된 파일을 작성하십시오.
9. 요약 테이블을 인쇄합니다.

## 입력 형식

이 스킬은 표준 팀 형식으로 내부 릴리스 노트를 수락합니다.

```
*ASO UI Release Notes — [Date Range]*
Collaborators: [teams]

✨ *Features*
• [Feature description]

🚀 *Enhancements*
• [Enhancement description]

🤖 *AI-First Development*
• [AI tooling items — will be dropped]

🔧 *Fixes & UX Improvements*
• [Fix description]

🏢 *BackOffice*
• [BackOffice items — will be dropped]
```

## 출력

스킬은 다음과 같은 결과를 출력합니다.

1. 서식 있는 고객 대면 항목(쓰기 전 검토용).
2. `release-notes.md`을(를) 수정하기 전에 확인 메시지를 표시합니다.
3. 쓰기 후: 보관/다시 작성/삭제된 항목의 요약 표.
