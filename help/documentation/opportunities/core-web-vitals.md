---
title: 핵심 웹 바이탈 기회 설명서
description: 핵심 웹 바이탈 기회에 대해 알아보고 이를 사용하여 트래픽 확보를 개선하는 방법을 알아봅니다.
badgeSiteHealth: label="사이트 상태" type="Caution" url="../../opportunity-types/site-health.md" tooltip="사이트 상태"
source-git-commit: fd992e5f4508ccd4236757167a16c744d98cc6ae
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 6%

---


# 핵심 웹 바이탈 기회

<!--![core web vitals opportunity](./assets/core-web-vitals/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483371/?learn=on&enablevpops)

Core Web Vitals 영업 기회는 사용자 경험과 유기 검색 성능에 영향을 미치는 웹 사이트의 페이지를 식별합니다. 이러한 문제는 사용자 지정 글꼴, 최적화되지 않은 JavaScript 종속성 및 서드파티 스크립트와 같은 요소에서 발생할 수 있습니다. Core Web Vitals은 컨텐츠 로드 속도, 페이지 레이아웃의 안정성 및 사용자 상호 작용에 대한 페이지의 반응성을 측정합니다.

AEM Sites Optimizer은 이러한 문제의 영향을 받는 페이지를 감지하고 코드 수준에서 특정 AI 권장 사항을 제공하며 기존 개발 워크플로를 통해 수정 사항을 적용합니다. 페이지 보기 수가 1,000개 이상인 페이지만 분석할 수 있습니다.

## 자동 식별

<!--![Auto-identify core web vitals](./assets/core-web-vitals/auto-identify.png){align="center"}-->

AEM Sites Optimizer은 [작동 원격 분석](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service)을 사용하여 LCP(최대 콘텐츠 페인트), CLS(누적 레이아웃 이동) 및 INP(다음 페인트로 상호 작용)와 같은 Core Web Vitals 지표에서 회귀를 감지하여 사이트 성능을 지속적으로 모니터링합니다. 실제 사용자 데이터를 사용하여 성능 회귀를 식별하고 사용자 경험에 미치는 영향에 따라 문제를 우선 지정합니다.

AEM Sites Optimizer은 모든 현재 문제 목록을 모바일 및 데스크톱별로 자세히 표시합니다. **페이지** 열은 영향을 받는 페이지 항목을 나타내며 문제는 LCP, INP 및 CLS로 분류됩니다.

## 자동 제안

<!--![Auto-suggest core web vitals opportunity](./assets/core-web-vitals/auto-suggest.png){align="center"}-->

식별된 각 문제에 대해 AEM Sites Optimizer은 규범적 코드 수준 권장 사항을 생성하여 Core Web Vitals 성능을 개선합니다. 코드 저장소에 액세스하여 기본 구현을 평가합니다. 이를 통해 구성 요소, 스크립트 및 스타일이 구현되는 방식을 분석하고 성능 문제의 근본 원인을 식별할 수 있습니다. 이 분석을 기반으로 시스템은 타깃팅된 권장 사항을 제공하고 성능 향상에 필요한 변경 사항을 지정하는 코드 패치를 생성합니다. 각 권장 사항은 적용되기 전에 검토할 수 있습니다.

제안 버튼을 클릭하면 성능 지표 LCP, INP 및 CLS를 범주로 포함하는 새 창이 나타납니다. 이러한 범주 간에 전환하여 특정 문제의 목록을 볼 수 있습니다. 각 카테고리에는 여러 문제가 포함될 수 있으므로 아래로 스크롤하여 문제 및 권장 사항의 전체 목록을 확인하십시오. 또한 각 지표에는 모바일과 데스크탑 모두에 대해 두 개의 성능 게이지가 있습니다.

## 자동 최적화

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

권장 사항을 검토하고 승인하면 **최적화 배포**&#x200B;를 클릭할 수 있습니다. AEM Sites Optimizer은 식별된 문제를 기반으로 코드 패치를 생성하고 버전 제어 프로세스를 통해 사용할 수 있도록 합니다. 최적화 프로세스에는 다음 단계가 포함됩니다.

* **문제 생성** - 명확한 설명과 가시성을 위해 영향을 받는 URL을 포함하여 각 수정 사항에 대해 레이블이 지정된 GitHub 문제를 만듭니다.
* **끌어오기 요청 배달** - 정확한 코드 수정 사항이 있는 연결된 끌어오기 요청을 자동으로 열고 검토, 테스트 및 병합할 준비가 되었습니다.
* **상태 추적** - 완료 과정을 통해 각 수정 사항을 추적하여 부분 또는 실패한 후속 조치 시도를 표시합니다.

AEM Sites Optimizer은 이러한 업데이트를 사용하기 전에 유효성 검사를 수행하여 수정 사항이 기본 문제를 해결하고 회귀를 초래하지 않는지 확인합니다. 모든 업데이트는 표준 개발 사례를 따르며 프로덕션으로 병합하기 전에 검토 및 승인이 필요합니다.

이를 통해 성능 최적화가 정확하고 검증되었으며 기존 개발 및 거버넌스 프로세스에 통합됩니다.
