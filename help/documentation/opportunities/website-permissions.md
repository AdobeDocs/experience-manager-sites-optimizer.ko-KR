---
title: 웹 사이트 권한 영업 기회 설명서
description: 웹 사이트 권한 기회에 대해 알아보고 이를 사용하여 웹 사이트의 보안을 강화하는 방법에 대해 알아봅니다.
badgeSecurityPosture: label="보안 태세" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="보안 태세"
source-git-commit: 5d1ae616ddde74f69b73ba5b44297c14b2dea36b
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 2%

---


# 웹 사이트 권한 기회

![웹 사이트 사용 권한 기회](./assets/website-permissions/hero.png){align="center"}

웹 사이트 권한 기회는 안전하고 관리하기 쉬운 AEM 환경을 유지하는 데 중요한 웹 사이트 권한을 최적화합니다. 이 기회를 사용하면 `/` 또는 `/content`과(와) 같은 일반 경로에서 `jcr:all`과(와) 같이 너무 광범위한 권한을 제거하고 사용자 액세스를 최소 권한의 원칙에 맞춰 액세스 제어를 세분화할 수 있습니다. 권한을 간소화하고 중복을 제거함으로써 보안 위험을 줄이고 유지 관리 가능성을 향상시키며 향후 오구성을 방지할 수 있습니다. AEM 보안 권한 콘솔 또는 코드 저장소에서 권한을 검토하고 업데이트하여 서비스 사용자가 진정으로 필요한 액세스 권한만 가질 수 있도록 합니다.

## 자동 식별

![웹 사이트 권한 자동 식별](./assets/website-permissions/auto-identify.png){align="center"}

**웹 사이트 권한 기회** 기능은 자동으로 식별되고 나열됩니다

* **사용자** - 의심스러운 권한이 있는 사용자 계정입니다.
* **경로** - 권한의 영향을 받는 AEM의 경로입니다.
* **권한** - 의심되는 권한입니다.
* **문제** - 권한에 영향을 주는 문제 유형을 나타냅니다.

## 자동 제안

![웹 사이트 자동 제안 취약점](./assets/website-permissions/auto-suggest.png){align="center"}

자동 제안은 **제안된 권한** 필드에 AI가 생성한 권장 사항을 제공하므로 플래그가 지정된 모든 권한을 보안 대체 권한으로 바꿀 수 있습니다.

## [!BADGE Ultimate] 자동 최적화{type=Positive tooltip="Ultimate"}

![웹 사이트 권한 자동 최적화](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimate은 발견된 취약점에 대해 자동 최적화 배포 기능을 추가합니다.

>[!BEGINTABS]

>[!TAB 최적화 배포]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 승인 요청]

{{auto-optimize-request-approval}}

>[!ENDTABS]
