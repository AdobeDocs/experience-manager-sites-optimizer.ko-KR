---
name: experience-league-video-upload
description: 사용자가 이 리포지토리의 Markdown에서 >[!VIDEO]를 통해 임베드하기 위해 Experience League(video.tv.adobe.com / KT 비디오 제출)에 비디오를 제출/업로드하려는 경우 사용합니다. 여기에는 브라우저 자동화로 제출 양식을 채우는 내용, 이 리포지토리의 기본값 및 자동화해서는 안 되는 사항이 포함됩니다.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# Experience League 비디오 업로드

## 개요

Experience League 비디오는 이 리포지토리에서 호스팅되지 않습니다. 로컬 `.mp4`이(가) 별도의 제출 양식을 통해 업로드됩니다. 이 양식은 `>[!VIDEO](...)`과(와) 함께 임베드된 `video.tv.adobe.com` URL을 반환합니다(&lbrack;[experience-league-markdown] 참조). 이 기술은 파일을 첨부하고 제출할 때까지 브라우저 자동화를 통해 해당 양식을 작성합니다.

양식: https://81368-exlmpcvideoupload.adobeio-static.net/#/

## 비디오 파일 추천

사용자가 클립을 기록하거나 선택하기 전에 **16:9 종횡비**&#x200B;을(를) **1920 x 1080픽셀의 최대 해상도**&#x200B;로 추천하십시오. 이는 스타일 기본 설정이 아니라 형식에서 지정한 요구 사항입니다. 요청을 받은 경우에만 사전에 언급하십시오(예: 사용자가 이를 위한 화면 녹화를 캡처하려고 할 때).

## 하드 규칙: 파일을 첨부하거나 제출하지 않음

제출하면 실제 KT Jira 티켓이 만들어지고 프로덕션 비디오 플랫폼으로 업로드됩니다. **항상** 다른 필드가 채워지면 중지하고 비디오 파일 및 최종 제출 클릭에 대해 사용자에게 다시 전달하십시오. 나중에 이 지침을 반복하지 않더라도 마찬가지입니다. 이는 이 스킬의 기본값이며, 요청별로 다시 확인해야 하는 것은 아닙니다. 사용자가 동일한 요청에서 해당 스킬에 대해 제출하라고 명시적으로 지시한 경우에만 이 중지를 건너뜁니다.

## 사전 요구 사항

이 저장소에 커밋된 **not**&#x200B;인 `chrome-devtools` MCP 서버가 필요합니다(브라우저 자동화 MCP는 모든 기여자에게 강제 적용해서는 안 됨). 로드되지 않은 경우:

1. 저장소 루트에 `.mcp.json` 만들기:

   ```json
   {
     "mcpServers": {
       "chrome-devtools": {
         "command": "npx",
         "args": ["-y", "chrome-devtools-mcp@latest", "--accept-insecure-certs", "--no-usage-statistics"]
       }
     }
   }
   ```

2. `.gitignore`에 `.mcp.json`을(를) 추가합니다(개인 도구, 공유되지 않음).
3. `.claude/settings.local.json`에서 `"enableAllProjectMcpServers": true` 및 `"enabledMcpjsonServers": ["chrome-devtools"]`을(를) 추가합니다.
4. 사용자에게 클라우드 코드를 다시 시작하도록 알립니다(또는 `/mcp` 실행). MCP 서버는 시작 시에만 로드되며, 세션 중간에 이 작업을 수행할 수 없습니다.

## 이 리포지토리의 기본값

사용자가 별도로 지정하지 않는 한 다음을 사용합니다.

| 필드 | 기본값 | 이유 |
|---|---|---|
| 클라우드 | `Experience Cloud` | — |
| 제품 | `AEM` | 이 리포지토리에 대한 사용자 지정 기본값(양식에 `AEM as a Cloud Service`도 나열됨 — 요청이 없는 경우 대체하지 않음) |
| 하위 제품 | `AEM Sites` | 가장 가까운 일치 항목, 양식에 &quot;Sites Optimizer&quot; 항목이 없습니다. |
| 역할 | `User` | Preflight/Sites Optimizer 콘텐츠는 비디오가 기술 사용자를 위한 것이 아니라면 관리자/개발자가 아닌 작성자/마케터를 대상으로 합니다 |
| 스킬 레벨 | `Beginner` | 표시된 워크플로우에 실제 사전 요구 사항이 있지 않은 경우 |
| 비디오 음성 성별 | `No voices` | 자동 화면 녹화에만 해당 - 클립에 내레이션이 있는지 묻습니다. |
| 비디오 유형 | 콘텐츠에서 묻기 또는 추론하기 | 라이브 옵션은 `Event` / `Feature` / `Technical` / `Value`입니다. UI 연습은 일반적으로 `Feature`입니다. |
| 이메일 | 미리 채워진 것 | 양식이 로그인한 사용자의 Adobe 이메일을 자동으로 채웁니다. 덮어쓰지 마십시오 |

## 단계

1. `mcp__chrome-devtools__new_page`을(를) 양식 URL로 복사합니다.
2. `mcp__chrome-devtools__take_snapshot`에서 양식 데이터 로드가 완료될 때까지 기다립니다(`"Title"`의 `mcp__chrome-devtools__wait_for`). &quot;양식 데이터 로드 중...&quot;에서 시작됩니다. 회전기.
3. **제목** 및 **설명** 채우기 — 설명은 일반 `<textarea>`이(가) 아닌 경합 가능한 서식 있는 텍스트 상자입니다. `fill`/`fill_form`이(가) 자동으로 작동하지 않습니다(값이 필요하지 않으며 &quot;필수&quot; 오류가 남아 있음). 대신 `click`을(를) 포커스로 설정한 다음 `mcp__chrome-devtools__type_text`을(를) 텍스트로 지정합니다.
4. 드롭다운(**비디오 유형**, **비디오 음성**, **클라우드**, **제품**, **하위 제품**, **이벤트 이름**)은 기본 `<select>`이 아닌 사용자 지정 목록 상자 단추입니다. 각 `click`에 대해 단추를 열려면 스냅숏에서 실제 옵션을 읽고(API로 로드됨 - 기본 테이블의 정확한 옵션 맞춤법이 최신 상태인 것으로 가정하지 않음) 일치하는 `option`을(를) `click`합니다.
5. **제품** 및 **하위 제품**&#x200B;은(는) 상위 필드가 설정될 때까지 비활성화됩니다(제품에 Cloud가 필요함, 하위 제품에 Product가 필요함). 해당 순서로 채우십시오.
6. **역할** 및 **스킬 수준**&#x200B;은(는) 확인란 그룹입니다. `uid` 확인란의 `"value": "true"`이(가) 있는 `fill_form`은(는) 설명 필드와 달리 여기에서 잘 작동합니다.
7. 그만해요 스크린샷을 캡처하여 설정한 내용과 이유(특히 제품/하위 제품과 같이 대체된 모든 기본값)를 요약하고, 사용자에게 비디오를 첨부하고 직접 제출하도록 알려줍니다.
8. 사용자가 제출했다고 하면 결과 Adobe MPC 비디오 URL(업로드 후 양식에 표시됨)을 요청합니다(예: `https://video.tv.adobe.com/v/3496629?learn=on`). 이 비디오가 재생될 때마다 `>[!VIDEO](...)` 바로 가기 코드를 채우십시오. URL/ID를 직접 조작하거나 추측하지 마십시오.

## 반환된 비디오 URL 유효성 검사

사용자가 포함할 비디오 URL을 제공할 때마다(위 8단계 또는 기타 시간):

- **`video.tv.adobe.com`에 없는 항목을 거부합니다.** 비디오가 [[experience-league-markdown]]에 따라 호스트되어야 합니다. YouTube, 파일 호스트 또는 다른 도메인에 대한 링크는 올바른 `>[!VIDEO]` 대상이 아닙니다. 이 리포지토리의 업로드 흐름을 먼저 거쳐야 한다고 사용자에게 알립니다. 임베드하지 마십시오.
- **유효한 `video.tv.adobe.com` URL에 `&enablevpops`이(가) 없으면 포함 전에**&#x200B;을(를) 추가하십시오. `help/home.md`, `help/documentation/trial.md` 등을 참조하여 이 리포지토리의 다른 `>[!VIDEO]`에서 이미 사용한 규칙과 일치합니다. `?`이(가) 이미 있으면 `&enablevpops`을(를) 추가하고, 그렇지 않으면 `?enablevpops`을(를) 추가합니다.

## 일반적인 실수

- 설명 필드에서 `fill`/`fill_form`을(를) 시도하고 오류 배너에 &quot;설명이 필요합니다&quot;라는 메시지가 계속 표시되면 진행합니다. — 종료뿐만 아니라 모든 단계 후에 오류 목록을 확인합니다.
- 드롭다운을 여는 대신 메모리에서 드롭다운 옵션 텍스트를 추측합니다. 실제 값(예: 음성 성별의 경우 `No voices`, 비디오 유형의 경우 `Feature`/`Technical`/`Value`, 제품에서 AEM/AEM-as-a-Cloud-Service 분할)은 이 문서와 독립적으로 추측하고 변경할 수 없습니다.
- **비디오 업로드**&#x200B;를 클릭하고 &quot;사용자를 한 단계 저장하려면&quot; 파일을 첨부합니다. 위의 Hard Rule을 참조하십시오.
