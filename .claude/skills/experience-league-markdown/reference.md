---
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---
# Experience League Markdown — 전체 구문 참조

https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax에서 압축됨("마지막 업데이트: 2026년 6월 17일" 페이지에 대해 마지막으로 확인됨). 여기에서 최신 상태가 아닌 것 같은 경우 라이브 페이지를 다시 가져옵니다.

## 전문 및 제목

```markdown
---
title: Title for search optimization
description: This is the article description used for search optimization.
---
# Article title
```

닫는 `---` 바로 뒤에 있는 줄(그리고 빈 줄 하나)은 `# Title`이어야 하며 앞뒤의 `title:`과(와) 일치해야 합니다.

## 기본 텍스트 서식

- 굵게: `**bold**`
- 기울임꼴: `*italic*`
- 굵은 기울임꼴: `***both***`
- 서식 문자 이스케이프 처리: `\*not italic\*`
- 단락에는 특별한 구문이 필요하지 않으며 단락 사이에 빈 줄만 있으면 됩니다.

## 제목

```markdown
# This is level 1 (article title)
## This is level 2 (mini-TOC entry)
### This is level 3
```

- `#`(H1) = 기사 제목이며 `title` 전문과 일치해야 합니다.
- `##`(H2) = 기본적으로 mini-TOC에 나타납니다(더 많은 수준을 표시하려면 frontmatter의 `mini-toc-levels: 3`).
- 수준을 건너뛰지 마십시오(`##` → `####`이(가) 잘못됨).
- 모든 제목 다음에 **및** 앞에 빈 줄이 필요합니다.
- 최대 제목 길이: 69자(EN), 120(지역화됨).
- 제목 ID/앵커: `## Creating processing rules {#processing-rules}` — 소문자로 하이픈이 연결되었습니다. 제목 텍스트가 숫자로 시작하는 경우 필요합니다(예: 연도). 명시적 ID가 없는 경우 기본 앵커는 자동 정렬 제목 텍스트입니다.

## 메모 / 지침

표준 형식: `NOTE`, `TIP`, `IMPORTANT`, `WARNING`. 최신 EXL 전용 형식: `ADMIN`, `AVAILABILITY`, `PREREQUISITES`, `INFO`, `ERROR`, `SUCCESS`.

```markdown
>[!NOTE]
>
>This is a standard NOTE block.
>
>It can include multiple paragraphs.
```

블록의 모든 줄은 `>`(으)로 시작합니다. 형식 마커 바로 뒤에 빈 `>` 줄을 포함하십시오.

## 탭

```markdown
>[!BEGINTABS]

>[!TAB iOS]

Content for the iOS tab.

>[!TAB Android]

Content for the Android tab.

>[!ENDTABS]
```

- 탭 집합 내의 탭 집합이나 목록 내의 탭 집합을 중첩할 수 없습니다.
- 탭 제목은 축어적으로 렌더링됩니다. `>[!TAB ...]` 내에서는 Markdown 서식이 없습니다.
- 여러 탭 세트는 한 페이지에서 사용할 수 있습니다.

## 비디오

```markdown
>[!VIDEO](https://video.tv.adobe.com/v/27069/?learn=on&enablevpops)
```

- 비디오가 `video.tv.adobe.com`(Adobe TV/MPC)에서 이미 호스팅되어야 합니다. 원시 비디오 파일 링크 또는 `<video>` 태그는 지원되지 않습니다.
- 권장 쿼리 매개 변수: `?learn=on&enablevpops`(이 저장소의 모든 임베드에 사용되는 표준 양식). 자동 재생에 `&autoplay=true`을(를) 추가합니다.
- 성적 증명서: 바로 가기 코드에 `{transcript=true}`을(를) 추가하거나 전체 안내서/리포지토리에 대해 `TOC.md`/`metadata.md`에서 `auto-video-transcripts: true`을(를) 설정합니다.

## 배지

인라인 배지(배치된 위치에서 렌더링):

```markdown
[!BADGE Beta]{type=Informative url="https://www.example.com" tooltip="Go to example.com"}
```

메타데이터 배지(H1 이상으로 렌더링됨) - 프론트매터:

```yaml
badgePremium: label="Premium" type="Positive" url="https://www.premium-product.com" tooltip="Download Premium"
```

- `type`(대/소문자 구분 안 함): `Informative`(기본값/파란색), `Positive`(녹색), `Negative`(빨간색), `Neutral`(진한 회색), `Caution`(노란색).
- 레이블만 필요합니다. `type`/`url`/`tooltip`은(는) 선택 사항입니다.
- 아티클당 최대 **2개** 메타데이터 배지(구성할 수 있지만 예외에 의존하기 전에 묻기).
- 메타데이터 배지 값은 따옴표로 묶어야 합니다. 인라인 배지 `url`/`tooltip`은(는) 따옴표로 묶어야 합니다.
- `TOC.md`에서 사용되는 배지 URL은 상대 URL이 아닌 루트 상대 URL(`/help/guide/article.md`)이어야 합니다. TOC 항목은 여러 폴더에 적용됩니다.
- `before-title="false"`이(가) 메타데이터 배지를 H1 아래로 이동합니다.
- `newtab=true`을(를) 추가하여 새 탭에서 배지 URL을 엽니다.

## 이미지

```markdown
![alt text](assets/logo.png "Hover text"){width="300" align="center"}
```

- `align`: `center` 또는 `right`만 — `left` 없음, `valign` 없음.
- `width`: 픽셀(`"300"`) 또는 보기 영역의 백분율(`"50%"`)입니다.
- `zoomable="yes"`이(가) 이미지를 클릭하여 확대하도록 만듭니다(또한 링크인 이미지와 결합하지 않음 - 링크가 성공함).
- 공유 이미지의 루트 상대 경로: `/help/assets/imagename.png`.
- 제한: 100MB 하드 캡(GitHub), 관리를 시작하기 5MB 전에 20MB가 유효성 검사 오류를 트리거합니다. 문서당 최대 100개의 이미지(EDS 렌더링 제한).

## 링크 및 상호 참조

- 외부: `[Adobe](https://www.adobe.com)`
- 링크로서의 기본 URL: `<https://www.adobe.com>` — 래핑되지 않은 기본 URL은 자동 링크되지 **않습니다**.
- 상대 상호 참조: `[Overview](collaborative-doc-instructions/overview.md)` — *source* 파일의 위치에서 확인되며, `./`, `../`, `../../`을(를) 지원합니다.
- 루트 상대 상호 참조: `[Overview](/help/using/docile-rules/introduction.md)` — 원본 위치에 관계없이 리포지토리의 모든 파일에서 작동합니다.
- 제목에 대한 딥링크: 대상에는 `{#heading-id}`이(가) 필요합니다. `[Text](file.md#heading-id)`(또는 동일한 페이지의 경우 `#heading-id`만)에 연결하십시오.
- 새 탭에서 열기: `[See What's new](whats-new.md){target="_blank"}`.

## 목록

```markdown
1. This is step 1.
1. This is the next step.
   1. Sub-step (indent 3 spaces for numbered lists)
   1. Sub-step
```

```markdown
* First item.
* Second item.
```

- 번호 매기기 목록: 항상 `1.` 쓰기(또는 항상 `1)`) — GitHub는 실제 시퀀스를 렌더링합니다. 한 스타일(`.`과 `)`)을 선택하고 문서 내에서 일관되게 유지하세요.
- 글머리 기호 목록: `*`, `-`, `+` 중 하나를 선택하고 일관되게 유지하십시오. 동일한 문서에서 이 글머리 기호를 혼합하면 유효성 검사 오류가 발생합니다. 대부분의 리포지토리에 있는 규칙: `*`.
- 목록 앞뒤에 빈 줄이 필요합니다.
- 목록 항목(이미지, 표, 메모) 사이의 내용은 텍스트 시작 부분(번호 매기기 목록의 경우 공백 3개, 글머리 기호 목록의 경우 공백 2개)으로 들여쓰거나 목록을 손상시켜야 합니다. 들여쓰기(6개 공백)를 사용하면 대신 코드 블록으로 바뀝니다.

## 코드 블록

인라인: `` `code` `` — 또는 내부에 리터럴 백틱이 필요한 경우 트리플 백틱 인라인으로 래핑합니다.

펜싱된:

&grave;&grave;&grave;&grave;markdown

```javascript
var x = 1;
```

&grave;&grave;&grave;&grave;

- 항상 구문 강조 표시 언어 + 복사 버튼을 지정합니다.
- 펜싱된 블록 위와 아래에 빈 줄이 필요합니다.
- 줄 번호: `` ``&#x200B;`html {line-numbers="true"} `&#x200B;&grave;
- 다른 곳에서 번호 매기기 시작: `` ``&#x200B;`html {line-numbers="true" start-line="7"} `&#x200B;&grave;
- 강조 표시 줄: `` ``&#x200B;`html {line-numbers="true" start-line="7" highlight="11-13, 16"} `&#x200B;&grave;
- 코드 블록 콘텐츠는 현지화되지 않습니다(게시 시 제거되는 `!UICONTROL`/`!DNL` 태그를 제외).
- Markdown/HTML 서식(예: `<i>`)은 코드 블록 내에서 작동하지 않습니다. 자리 표시자에는 꺾쇠 괄호 또는 일반 텍스트를 사용하십시오.

## 표

- 표준 GFM 파이프 테이블은 간단한 경우에 사용할 수 있습니다.
- HTML 테이블은 특별한 경우에 허용됩니다(예: 헤더 행이 없는 테이블). 그렇지 않으면 markdown을 선호합니다.
- Markdown 테이블 셀 내에서 제한된 HTML이 허용됩니다. `<p>`, `<br>`, `<ul>`, `<ol>`.
- 표는 자동 렌더링 또는 고정 렌더링으로 설정할 수 있습니다. 해당 제어 수준이 필요한 경우 구문 안내서에서 연결된 &quot;표&quot; 문서를 참조하십시오.

## 축소 가능한 섹션

```markdown
+++See details

This is text inside a collapsible section.

* Bullet one
* Bullet two

+++
```

- 축소 가능한 섹션은 중첩하지 않습니다. - 올바르게 렌더링되지 않으며 유효성 검사에 실패하지 않으므로 버그가 자동으로 제공됩니다.
- 섹션 내의 내부 목록/코드 블록 주위에 빈 줄이 있어야 합니다. 다른 곳과 동일합니다.

## 텍스트 강조 표시

```markdown
This sentence is normal. <span class="preview">This text is highlighted.</span>
```

인라인/단락 강조 표시에는 `<span class="preview">`을(를) 사용하고 여러 단락/구성 요소에는 `<div class="preview">`을(를) 사용합니다.

## 코드 조각 및 포함

- 리포지토리의 `help/snippets.md`에서 H2 앵커를 공유했습니다. `{{anchor-id}}`을(를) 사용한 참조입니다.
- `help/_includes/*.md`의 포함 파일을 공유했습니다. `{{$include /help/_includes/filename.md}}`과(와) 함께 참조합니다.

## 댓글

```markdown
<!-- standard comment code -->
```

- `<!--> bad comment syntax <-->`을(를) 사용하지 마십시오(대시 누락). 텍스트를 숨기는 대신 시각적으로 렌더링됩니다.
- 주석은 렌더링된 문서에서 볼 수 없지만 **GitHub에서 원시 .md를 보는 모든 사람에게 볼 수 있음** — 비밀 또는 기밀 정보가 없음.
- 글머리 기호 목록 내에 주석을 사용하지 마십시오(목록 렌더링을 중단할 수 있음). `TOC.md`에서 파일 끝에 있는 줄만 주석 처리하십시오. 목록 가운데에는 주석을 추가할 수 없습니다.

## 빈 라인 해결 방법

소스에 있는 추가 빈 선은 렌더러에 의해 축소됩니다. 표시 세로 공백을 강제 적용하려면 간격을 원하는 줄에 `<br>&nbsp;`을(를) 넣습니다.

## 문자 이스케이프 처리

- 백슬래시 사용 가능 문자: `` # { } [ ] * + - . ! ``(예: `\# not a heading`).
- 꺾쇠 괄호(`<placeholder>`)의 경우 백슬래시가 작동하지 않습니다. 인라인 코드 블록(`` `<placeholder>` ``) 또는 HTML 엔터티(`&lt;placeholder&gt;`)를 사용하십시오.
- 코드 블록 내의 HTML 엔터티가 **not** 문자로 다시 변환되었습니다. `&gt;`은(는) 리터럴 텍스트를 그대로 유지합니다.
- 메타데이터(YAML Frontmatter)에는 자체 이스케이프 규칙이 있습니다. 값이 `:` 또는 `[`과(와) 같은 특수 문자로 시작하는 경우 전체 값을 따옴표로 묶습니다. `title: "Processing rules: A new beginning"`.

## 제한된 HTML

이러한 HTML 태그만 Markdown의 어디에서나 허용됩니다. 그 외의 다른 태그는 유효성 검사 오류입니다.

```
table  tbody  td  tfoot  thead  th  tr  col  colgroup
p  ul  ol  li  br
b  i  strong  u  s  em  sub  sup  span
caption  a  img  div
pre  code  codeblock
```

Markdown으로 작업을 수행할 수 있는 모든 곳에서 HTML보다 Markdown 구문을 선호합니다. HTML은 실제로 헤더가 없는 테이블과 같은 극단적인 사례에만 사용됩니다.

## 명시적으로 지원되지 않음(로컬 미리 보기에서 렌더링하더라도 사용하지 않음)

- 가로 규칙(`***`, `<hr>`)
- 이모지 바로 가기 코드(`:bowtie:`)
- 작업 목록(`- [x] done`)
- 참고/탭/비디오 바로 가기 코드(일반 `>` 블록 따옴표는 스타일이 지정된 구성 요소가 아닌 견적으로 렌더링) 너머 블록 따옴표 *구성 요소*
- Markdown 정의 목록 구문(대신 수동 굵게 + 대시 서식 사용: `**Frog** - An amphibious green creature.`)
- 이미지의 `valign`

## 알 만한 가치가 있는 파일 크기/개수 제한

| Thing | 제한 |
|---|---|
| 이미지/다운로드 파일 크기 | 5MB의 유효성 검사 경고, 20MB의 오류, 하드 GitHub 캡 100MB |
| 기사당 이미지 수 | 100(EDS 렌더링 제한) |
| 기사당 메타데이터 배지 | 2(기본값) |
