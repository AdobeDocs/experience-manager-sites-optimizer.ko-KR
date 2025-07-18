---
title: Sites Optimizer로 보안 태세 최적화
description: Sites Optimizer로 사이트의 보안을 개선하는 방법을 알아봅니다.
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 89%

---


# 보안 태세 기회

![보안 태세 기회](./assets/security-posture/hero.png){align="center"}

AEM Sites Optimizer에서 강력한 보안 태세를 유지하는 것은 디지털 경험과 사용자 데이터를 보호하는 데 중요합니다. CORS 구성, 크로스 사이트 스크립팅, 웹 사이트 권한 및 웹 사이트 취약점 등과 같은 개선 기회를 식별함으로써 팀은 잠재적인 보안 위험을 사전에 해결하고 모범 사례를 준수할 수 있습니다. 보안 조치를 강화하면 민감한 정보를 보호할 수 있을 뿐만 아니라 사용자 신뢰와 사이트 안정성도 향상됩니다. AEM Sites Optimizer의 통찰력을 사용하면 조직은 보안 상태를 지속적으로 모니터링하고 개선하여 위험을 줄이고 안전한 디지털 환경을 유지할 수 있습니다.

## 기회


<!-- CARDS

* ../documentation/opportunities/cors-configuration.md
  {title=CORS configuration}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/cross-site-scripting.md
  {title=Cross-site scripting}
  {image=../assets/common/card-gear.png}
* ../documentation/opportunities/website-permissions.md  
  {title=Website permissions}
  {image=../assets/common/card-people.png}
* ../documentation/opportunities//website-vulnerabilities.md
  {title=Website vulnerabilities}
  {image=../assets/common/card-puzzle.png}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="CORS configuration">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/cors-configuration.md" title="CORS 구성" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="CORS 구성"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/cors-configuration.md" target="_blank" rel="referrer" title="CORS 구성">CORS 구성</a>
                    </p>
                    <p class="is-size-6">CORS 구성 기회에 대해 알아보고 사이트 보안 취약점을 식별하여 해결하는 방법을 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/cors-configuration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Cross-site scripting">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/cross-site-scripting.md" title="크로스 사이트 스크립팅" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-gear.png" alt="크로스 사이트 스크립팅"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/cross-site-scripting.md" target="_blank" rel="referrer" title="크로스 사이트 스크립팅">크로스 사이트 스크립팅</a>
                    </p>
                    <p class="is-size-6">크로스 사이트 스크립팅 기회에 대해 알아보고 사이트 보안 취약점을 식별하여 해결하는 방법을 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/cross-site-scripting.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Website permissions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/website-permissions.md" title="웹 사이트 권한" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-people.png" alt="웹 사이트 권한"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/website-permissions.md" target="_blank" rel="referrer" title="웹 사이트 권한">웹 사이트 권한</a>
                    </p>
                    <p class="is-size-6">웹 사이트 권한 기회와 이를 사용하여 웹 사이트 보안을 강화하는 방법을 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities/website-permissions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Website vulnerabilities">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities//website-vulnerabilities.md" title="웹 사이트 취약점" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-puzzle.png" alt="웹 사이트 취약점"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" title="웹 사이트 취약점">웹 사이트 취약점</a>
                    </p>
                    <p class="is-size-6">웹 사이트 취약점 기회와 이를 사용하여 웹 사이트 보안을 강화하는 방법을 알아봅니다.</p>
                </div>
                <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">자세히 알아보기</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


