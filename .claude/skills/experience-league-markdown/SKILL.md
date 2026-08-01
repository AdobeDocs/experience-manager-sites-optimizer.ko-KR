---
name: experience-league-markdown
description: Adobe Experience League/Adobe-Enterprise-Docs 리포지토리(help/**/*.md)에서 Markdown 파일을 작성하거나 편집할 때 사용합니다. — 프론트마스트, 제목, 메모(NOTE/TIP/IMPORTANT/WARNING/etc), 탭(BEGINTAB/TAB/ENDTAB), 비디오 포함, 배지, 이미지, 링크/상호 참조, 테이블, 목록, 코드 블록 및 Experience League의 유효성 검사 힘에 대한 제한된 HTML 태그/엔드탭을 제어합니다.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Experience League Markdown

## 개요

Experience League 문서는 GitHub 버전의 Markdown과 일련의 사용자 지정 확장 기능(블록 인용 기반 단축 코드, 배지, 탭, 비디오 임베드)을 사용합니다. 작성 파이프라인 **이러한 파일을 확인**&#x200B;합니다. 지원되지 않는 구문(원시 `<video>` 태그, `<hr>`, 작업 목록, 혼합 글머리 기호 문자, 건너뛴 제목 수준, 크기 초과된 이미지)을 사용하면 스타일 단위뿐만 아니라 빌드/유효성 검사 오류가 발생합니다.

Source of truth: https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax (local reference.md가 오래된 것 같은 경우 이 페이지를 가져오십시오. &quot;마지막 업데이트&quot; 날짜가 맨 위에 있습니다.)

모든 바로 가기 코드와 규칙을 사용한 전체 구문 참조: [reference.md](reference.md). 사소하지 않은 항목(탭, 비디오, 배지, HTML이 포함된 표)을 작성하기 전에 읽으십시오.

## 빠른 참조

| 요소 | 구문 | 메모 |
|---|---|---|
| 프론트메터 | `---\ntitle: ...\ndescription: ...\n---` | 빈 줄, `# Title`이(가) 다음에 와야 함 |
| 제목 수준 | `#`, `##`, `###` | `#` = 제목(`title`과 일치), `##` = mini-TOC 항목. 레벨을 절대 건너뛸 수 없습니다. 앞/뒤에 빈 줄. 최대 69자(EN) |
| 제목 ID | `## Heading text {#custom-id}` | 제목이 숫자로 시작하거나 숫자를 포함하는 경우 필요합니다(예: `## 2026 release notes {#2026-release-notes}`). |
| 메모/팁/기타 | `>[!NOTE]`, `>`, `>Text`(각각 고유한 줄에 있음) | 유형: 참고, 팁, 중요, 경고, 주의, 관리자, 가용성, 사전 요구 사항, 정보, 오류, 성공 |
| 탭 | `>[!BEGINTABS]` / `>[!TAB Title]` / `>[!ENDTABS]` | 탭 집합을 중첩할 수 없으며 목록 내에 중첩할 수 없습니다. |
| 비디오 | `>[!VIDEO](https://video.tv.adobe.com/v/ID/?learn=on&enablevpops)` | video.tv.adobe.com에서 호스팅해야 합니다. 원시 `<video>`/파일 링크가 없습니다. |
| 이미지 | `![alt text](assets/img.png "hover text"){width="300" align="center"}` | `align`은(는) `center` 또는 `right`만(`left`, `valign` 없음) |
| 링크(상대) | `[Text](../folder/file.md)` | 소스 파일 위치 계정 |
| 링크(루트) | `[Text](/help/guide/file.md)` | 저장소 내 어디에서나 작동합니다. TOC.md 배지 URL에 필요합니다. |
| 딥링크 | `[Text](file.md#heading-id)` | 대상 머리글에는 명시적 `{#heading-id}`이(가) 필요합니다. |
| 외부 링크(빈 URL) | `<https://example.com>` | 기본 URL이 자동으로 연결되지 않습니다. `< >`을(를) 래핑하거나 `[text](url)`을(를) 사용하십시오. |
| 글머리 기호 목록 | `* item`(`*`/`-`/`+` 중 하나 선택, 일관성 유지) | 목록 앞/뒤에 빈 줄, 혼합 마커 = 유효성 검사 오류 |
| 번호 매기기 목록 | `1. item`(줄마다 `1.` 반복) | GitHub에서 실수 렌더링 |
| 코드(인라인) | `` `code` `` | 파일 이름, 명령, 값, 검증되지 않은 샘플 URL의 경우 |
| 코드(펜싱) | ` `&#x200B;``language ` ... ` ``&#x200B;` ` | 항상 언어 지정, 앞/뒤에 빈 줄 지정, `{line-numbers="true" start-line="n" highlight="n-m"}` 선택 사항 |
| 배지(인라인) | `[!BADGE Beta]{type=Informative url="..." tooltip="..."}` | `type`: 정보/양수/음수/중립/주의 |
| 접기 가능 | `+++Summary` ... `+++` | 중첩된 축소 가능 항목 없음, 내부 목록/코드 주위에 빈 줄 표시 |
| 빈 줄 해킹 | `<br>&nbsp;`(줄 바꿈) | 렌더러에서 일반 추가 빈 줄을 축소/무시합니다 |
| 댓글 | `<!-- text -->` | `<!--> text <-->` 사용 안 함 — GitHub에서 원시 파일을 보는 모든 사람이 볼 수 있으므로 비밀이 없습니다. |

## 일반적인 실수

- **원시 `<video>`, `<iframe>` 또는 기타 허용 목록에추가된이 아닌 HTML**→ 유효성 검사 오류입니다. HTML 허용 목록: `table tbody td tfoot thead th tr col colgroup p ul ol li br b caption i strong u s span sub sup a img div em pre code codeblock` 다른 모든 항목(`<video>`/`<source>` 포함)은 거부됩니다. 대신 `>[!VIDEO]` 바로 가기 코드를 사용하십시오. 이 경우 비디오가 이미 video.tv.adobe.com에서 호스팅되어야 합니다.
- **`<hr>`/ `***` 가로 규칙, 이모지 바로 가기 코드(`:bowtie:`), 작업 목록(`- [x]`)** — 모두 지원되지 않습니다. 로컬 미리 보기에서 렌더링하더라도 사용하지 마십시오.
- **글머리 기호 문자 혼합**(`*` 및 `-`이(가) 같은 목록에 있음) — 유효성 검사 오류입니다. 기사당 하나를 고르세요.
- **제목 수준 건너뛰기**(`####`(으)로 `##`) — 허용되지 않습니다.
- **명시적 ID가 없는 숫자 행간 제목**(예: `## 2026 release notes`) — `{#some-id}`을(를) 추가해야 합니다. 그렇지 않으면 자동 슬러그가 충돌/중단될 수 있습니다.
- **산문의 URL 없음**(`Visit https://example.com for more`) — 링크로 렌더링되지 않습니다. `< >`에서 래핑하거나 `[text](url)`을(를) 사용합니다.
- **시각적 간격에 대한 추가 빈 줄** — 렌더러에서 축소되었습니다. 빈 `<br>` 또는 반복되는 줄 바꿈 대신 `<br>&nbsp;` 사용
- **이미지 ~5MB** — 5MB에서 유효성 검사 경고, 20MB에서 오류. 한 문서에서 100개 이상의 이미지가 렌더링을 중단합니다(EDS 제한).
- **Frontmatter 메타데이터에 두 개 이상의 배지가 있습니다** — 기본적으로 허용되지 않습니다.
- **문제 이스케이프**: 백슬래시 이스케이프는 `` # { } [ ] * + - . ! ``에만 작동합니다. `<filename>` 자리 표시자와 같은 항목의 `<` `>`에 대해 백슬래시가 아닌 인라인 코드 블록 또는 HTML 엔터티(`&lt;filename&gt;`)를 사용하십시오.

## Markdown 변경 사항을 커밋하기 전

1. Frontmatter가 있으면 `# Title`이(가) 바로 뒤에 옵니다(빈 줄 뒤).
2. 모든 머리글에는 이전과 이후에 빈 줄이 있으며, 건너뛴 수준은 없습니다.
3. 모든 비디오는 원시 `<video>` 태그가 아닌 `>[!VIDEO](https://video.tv.adobe.com/...)`입니다.
4. 모든 사용자 지정 바로 가기 코드(`>[!NOTE]`, `>[!BEGINTABS]`, `>[!BADGE ...]`)가 [reference.md](reference.md)의 정확한 구문과 일치합니다(여러 줄 블록 내에 빈 `>` 줄 포함).
5. 목록은 전체 목록 주위에 빈 줄이 있는 일관된 글머리 기호/번호 스타일을 사용합니다.
6. 링크: 상대 링크는 *source* 파일의 폴더에서 확인됩니다. 교차 리포지토리 또는 TOC/배지 링크는 루트 상대(`/help/...`) 양식을 사용합니다.
7. 위의 일반적인 실수 섹션에서 HTML 외부에 태그를 지정하지 마십시오.
