---
title: 웹 사이트 권한 기회 설명서
description: 웹 사이트 권한 기회와 이를 사용하여 웹 사이트 보안을 강화하는 방법을 알아봅니다.
badgeSecurityPosture: label="보안 태세" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="보안 태세"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 79%

---


# 웹 사이트 권한 기회

![웹 사이트 권한 기회](./assets/website-permissions/hero.png){align="center"}

웹 사이트 권한 기회는 안전하고 관리하기 쉬운 AEM 환경을 유지하는 데 요소인 중요한 웹 사이트 권한을 최적화합니다. 이 기회를 통해 지나치게 광범위한 권한(예: `/` 또는 `/content` 등 일반 경로에 있는 `jcr:all`)을 제거하고 사용자 액세스를 최소 권한 원칙에 맞춰 조정하여 액세스 제어를 개선할 수 있습니다. 권한을 간소화하고 중복을 제거하면 보안 위험을 줄이고, 유지 가능성 개선하고, 향후 잘못된 구성을 방지할 수 있습니다. AEM 보안 권한 콘솔 또는 코드 저장소에서 권한을 검토하고 업데이트합니다. 이렇게 하면 서비스 사용자가 진정으로 필요한 액세스 권한만 갖게 됩니다.

## 자동 식별

![웹 사이트 권한 자동 식별](./assets/website-permissions/auto-identify.png){align="center"}

**웹 사이트 권한 기회** 기능은 다음을 자동으로 식별하고 나열합니다.

* **사용자** – 의심스러운 권한이 있는 사용자 계정입니다.
* **경로** - 맨 위의 탭을 사용하여 상태별로 기회를 구성하고 필터링합니다.
* **권한** - 의심되는 권한입니다.
* **문제** - 권한에 영향을 미치는 문제의 유형을 나타냅니다.

## 자동 제안

![웹 사이트 취약점 자동 제안](./assets/website-permissions/auto-suggest.png){align="center"}

자동 제안 기능은 **제안된 권한** 필드에 AI가 생성한 권장 사항을 제공하여 플래그가 지정된 권한을 안전한 대체 권한으로 바꿀 수 있도록 해 줍니다.

## 자동 최적화

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![웹 사이트 권한 자동 최적화](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimate에는 발견된 취약점에 대해 자동 최적화를 배포하는 기능이 추가됩니다.

>[!BEGINTABS]

>[!TAB 최적화 배포]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 승인 요청]

{{auto-optimize-request-approval}}

>[!ENDTABS]
