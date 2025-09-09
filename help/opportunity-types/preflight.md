---
title: AEM Sites Optimizer - Preflight 온보딩 안내서
description: AEM Sites Optimizer에서 Preflight 기회 및 Preflight 분석을 설정하는 방법에 대해 알아봅니다.
source-git-commit: 0a6ddcdfd369253500067b31617facfb7f38b656
workflow-type: ht
source-wordcount: '488'
ht-degree: 100%

---


# Preflight 기회

![Preflight 기회](./assets/preflight/hero.png){align="center"}

<span class="preview">AEM Sites Optimizer Preflight는 페이지의 기술 및 성능 데이터를 분석하고 게시되기 전에 기회를 예측하고 감지합니다. 생성형 AI를 사용하여 최적화를 제안합니다.</span>

## 기회

<!-- CARDS

* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Canonical}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/broken-internal-links.md
  {title=Broken Internal Links}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Metatags}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=H1 count}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/accessibility-issues.md
  {title=Accessibility}
  {image=../assets/common/card-puzzle.png}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Canonical">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="표준" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="표준"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="표준">표준</a>
                    </p>
                    <p class="is-size-6">표준 기회에 대해 알아보고 이를 사용하여 SEO를 개선하고 중복 콘텐츠 문제를 방지하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken Internal Links">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/broken-internal-links.md" title="끊어진 내부 링크" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="끊어진 내부 링크"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" title="끊어진 내부 링크">끊어진 내부 링크</a>
                    </p>
                    <p class="is-size-6">끊어진 내부 링크 기회에 대해 알아보고, 이를 사용하여 웹 사이트의 끊어지거나 문제가 있는 링크를 식별하고 수정하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Metatags">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="메타태그" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="메타태그"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="메타태그">메타태그</a>
                    </p>
                    <p class="is-size-6">메타태그 기회에 대해 알아보고, 더 나은 SEO 성능을 위해 메타태그를 사용하여 페이지의 메타데이터를 최적화하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="H1 count">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="H1 수" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="H1 수"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="H1 수">H1 수</a>
                    </p>
                    <p class="is-size-6">H1 수 기회에 대해 알아보고 이를 사용하여 적절한 헤딩 구조 및 SEO 최적화를 보장하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Accessibility">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/accessibility-issues.md" title="접근성" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-puzzle.png" alt="접근성"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" title="접근성">접근성</a>
                    </p>
                    <p class="is-size-6">접근성 기회에 대해 알아보고, 모든 사용자가 웹 사이트에 액세스할 수 있도록 접근성 기회를 활용하는 방법에 대해 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>

</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 설정 방법

### 범용 편집기 설정

1. URL https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor에서 Extension Manager로 이동합니다.
2. AEM Sites Optimizer Preflight 확장 기능을 선택하고 활성화를 요청합니다.
3. AEM 팀이 조직에 대한 확장 기능을 활성화합니다.
4. 완료되면 https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/site/subscription.html과 같은 페이지를 범용 편집기에서 엽니다.
5. Preflight 확장 기능이 사이드 레일에 표시됩니다.
6. 사이드 레일에서 Preflight 확장 기능을 클릭하면 현재 페이지에 대한 Preflight 감사가 시작됩니다.

### 문서 기반 미리보기 설정

#### 1단계: Preflight 버튼으로 Sidekick 활성화

GitHub 저장소의 `/tools/sidekick/config.json`에 다음 구성을 추가합니다.

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

#### 2단계: Sidekick 통합 스크립트 만들기

다음 콘텐츠로 `/tools/sidekick/aem-sites-optimizer-preflight.js`s를 만듭니다.

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

#### 3단계: 스크립트 파일 업데이트

미리보기 URL에 대해 `/scripts/scripts.js`의 `loadLazy()` 함수에 아래에 표시된 대로 다음 import 문을 추가합니다.

```javascript
if (window.location.href.includes('.aem.page')) {
   import('../tools/sidekick/aem-sites-optimizer-preflight.js');
}
```

이제 Preflight 버튼이 Sidekick에 표시됩니다.

#### 4단계: 감사 실행

감사된 페이지의 미리보기 URL(*.aem.page)을 엽니다. Sidekick에서 Preflight 버튼을 클릭합니다.

### AEM Cloud Service 설정

북마클릿 옵션을 사용하면 AEM Cloud Service 페이지 편집기 및 샌드박스 환경에서 Preflight를 테스트할 수 있습니다.

<!-- Drag the button below to your Bookmarks Bar to get started. -->

북마크 바를 표시하려면 **Ctrl+Shift+B**(Windows) 또는 **Cmd+Shift+B**(Mac)를 누르십시오. 북마크 바를 마우스 오른쪽 버튼으로 클릭하고 “새 페이지” 또는 “북마크 추가”를 선택합니다. 주소 필드에 아래 코드를 복사합니다.

<!-- **Drag this link to your Bookmarks Bar:**

<a href="javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();">Preflight</a> -->

**이 코드를 복사하여 새 북마크를 만듭니다.**

```
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

북마클릿이 추가되면 감사된 페이지의 미리보기 URL(*.aem.page)을 엽니다. Preflight 북마크를 클릭하여 Preflight 감사를 시작합니다.

## 모범 사례

Preflight를 사용할 때는 다음 사항에 유의하십시오.

* 게시하기 전에 모든 스테이징/미리보기 페이지에서 Preflight 감사를 실행합니다.
* 영향력이 큰 문제(끊어진 링크, 누락된 H1 태그, 안전하지 않은 링크)를 먼저 해결합니다.
* 보호된 스테이징 환경에 대해 인증을 활성화합니다.
* 더 나은 SEO 성능을 위해 메타태그 제안을 검토하고 구현합니다.
