---
title: Preflight 설정
description: AEM Sites Optimizer용 Preflight 확장을 설정하는 방법을 알아봅니다.
source-git-commit: 210acc5337796707ced10f2b84d473503fc06088
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 100%

---


# Preflight 설정

AEM Sites Optimizer Preflight 기회 식별을 위해서는 범용 편집기, 문서 기반 미리 보기 또는 AEM Cloud Service에서 Preflight 확장 기능을 설정해야 합니다. 이를 통해 페이지가 게시되기 전에 Preflight 감사를 실행할 수 있습니다.

## 사용자 액세스 활성화

Preflight 확장 기능을 사용하려면 사용자가 [Adobe Admin Console](https://adminconsole.adobe.com)에서 다음과 같은 AEM Sites Optimizer 제품 프로필 중 하나 이상에 할당되어 있는지 확인하십시오.

* AEM Sites Optimizer - 사용자 자동 제안
* AEM Sites Optimizer - 사용자 자동 최적화

## Preflight 확장 기능 활성화

>[!BEGINTABS]

>[!TAB 범용 편집기]

범용 편집기에서 Preflight 기능을 설정하려면 다음과 같은 단계를 따릅니다.

1. 다음 위치에서 **Extension Manager**를 엽니다.
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. **AEM Sites Optimizer Preflight 확장 기능**&#x200B;의 위치를 확인하고 활성화를 위한 요청을 제출합니다.
1. **Adobe AEM 팀**&#x200B;이 조직에 대한 확장 기능을 검토하고 활성화합니다.
1. 확장 기능 활성화 후 **범용 편집기**에서 페이지를 하나 엽니다. 예:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. **Preflight 확장 기능**&#x200B;이 **사이드 레일**&#x200B;에 나타납니다.
1. 사이드 레일에서 **Preflight 확장 기능**&#x200B;을 선택하여 현재 페이지의 **Preflight 감사**&#x200B;를 시작합니다.

>[!TAB 문서 기반 작성]

문서 기반 작성을 위해 Preflight를 설정하려면 다음과 같은 단계를 따릅니다.

1. Edge Delivery Services 프로젝트의 GitHub 저장소에서 `/tools/sidekick/config.json`에 다음과 같은 구성을 추가합니다.

   ```json
   {
     "plugins": [
       {
         "id": "preflight",
         "titleI18n": {
           "en": "Preflight"
         },
         "environments": ["preview"],
         "event": "preflight"
       }
     ]
   }
   ```

1. 새 파일(`/tools/sidekick/aem-sites-optimizer-preflight.js`)을 만들고 다음과 같은 내용을 추가합니다.

   ```javascript
   (function () {
     let isAEMSitesOptimizerPreflightAppLoaded = false;
     function loadAEMSitesOptimizerPreflightApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMSitesOptimizerPreflightAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMSitesOptimizerPreflightApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMSitesOptimizerPreflightAppLoaded) {
         loadAEMSitesOptimizerPreflightApp();
       }
     }
   
     // Sidekick V1 extension support
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       sidekick.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   
     // Sidekick V2 extension support
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       sidekickV2.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. 다음과 같이 `/scripts/scripts.js`에서 `loadLazy()` 함수를 업데이트하여 미리보기 URL에 대한 Preflight 스크립트를 가져옵니다.

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. 감사하려는 페이지의 미리보기 URL(`*.aem.page`)을 엽니다.
1. **Sidekick**&#x200B;에서 **Peflight** 버튼을 클릭하여 현재 페이지에 대한 감사를 시작합니다.

>[!TAB AEM Sites 페이지 편집기]

AEM Sites 페이지 편집기에서 Preflight를 사용하기 위해 웹 브라우저 내에 북마클릿을 만들 수 있습니다. 다음 단계를 수행하십시오.

1. 다음과 같이 웹 브라우저에 **북마크 바**&#x200B;를 표시합니다.

   * **Ctrl+Shift+B**(Windows) 또는 **Cmd+Shift+B**(Mac)를 누릅니다.

1. 다음과 같이 브라우저에 새 북마크를 만듭니다.

   * 북마크 바를 마우스 오른쪽 버튼으로 클릭하고 **새 페이지** 또는 **북마크 추가**&#x200B;를 선택합니다.
   * **주소(URL)** 필드에 다음 코드를 붙여 넣습니다.

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. 북마크의 이름을 **Preflight**(또는 원하는 이름)로 지정합니다.
1. **AEM Sites 페이지 편집기**&#x200B;에서 감사하려는 페이지의 미리보기 URL(`*.aem.page`)을 엽니다.
1. 북마크 바에서 **Preflight** 북마크를 클릭해 현재 페이지에 대한 감사를 시작합니다.

>[!ENDTABS]

## 모범 사례

Preflight 감사를 실행 시 다음과 같은 지침을 염두에 두십시오.

* 프로덕션에 게시하기 전 항상 **스테이징 페이지 또는 미리보기 페이지**&#x200B;에서 감사를 실행하십시오.
* 끊어진 링크, 누락된 H1 태그, 안전하지 않은 링크 등 **큰 영향력을 갖는 문제** 해결을 우선시하십시오.
* 감사 실행 전 보호된 스테이징 환경에 대한 **인증이 활성화**&#x200B;되어 있는지 확인하십시오.
* **메타 태그 권장 사항**&#x200B;을 검토 및 적용하여 SEO 성능을 개선하십시오.
