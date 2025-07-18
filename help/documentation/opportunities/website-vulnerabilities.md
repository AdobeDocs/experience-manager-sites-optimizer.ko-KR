---
title: 웹 사이트 취약점 기회 설명서
description: 웹 사이트 취약점 기회와 이를 사용하여 웹 사이트 보안을 강화하는 방법을 알아봅니다.
badgeSecurityPosture: label="보안 태세" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="보안 태세"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 77%

---


# 웹 사이트 취약점 기회

![웹 사이트 취약점 기회](./assets/website-vulnerabilities/hero.png){align="center"}

웹 사이트 취약성 기회는 애플리케이션 코드에서 사용하는 서드파티 라이브러리의 보안 취약성을 식별합니다. 악의적인 공격자는 이러한 취약점을 악용하여 위험을 높이고 웹 사이트의 보안 자세를 낮춥니다.

웹 사이트 취약점 기회는 페이지 상단에 다음 내용을 포함한 요약을 표시합니다.

* **발견된 문제** – 발견된 취약점의 수를 보안 위험에 따라 분류(낮음, 보통, 높음)합니다.
* **집계된 보안 위험** – 기회를 통해 발견된 취약점을 기반으로 한 웹 사이트의 전반적인 보안 위험입니다.

## 자동 식별

![웹 사이트 취약점 자동 식별](./assets/website-vulnerabilities/auto-identify.png){align="center"}

**웹 사이트 취약점 기회** 기능은 애플리케이션 코드에서 사용하는 서드파티 라이브러리에서 발견된 취약점을 자동으로 식별하여 나열합니다. 다음과 같은 세부 정보가 제공됩니다.

* **라이브러리** – 취약점이 포함된 서드파티 라이브러리입니다. 단일 라이브러리에도 여러 개의 취약점이 있을 수 있습니다.
* **현재 버전** – 현재 사용 중인 라이브러리 버전입니다.
* **권장 버전** – 취약점을 해결하는 제안된 버전입니다.
* **점수** – 취약점의 심각도 순위이며 페이지 상단에 요약되어 있습니다.
* **취약점** – 취약점 식별자, 간략한 설명 및 세부 정보를 위한 NVD(National Vulnerability Database)에 대한 링크를 제공합니다. 식별자나 설명 옆에 있는 링크를 클릭하여 NVD 링크에 액세스하십시오.

## 자동 제안

![웹 사이트 취약점 자동 제안](./assets/website-vulnerabilities/auto-suggest.png){align="center"}

자동 제안은 업그레이드해야 하는 취약한 라이브러리의 **권장 버전**&#x200B;에 대한 AI 생성 제안을 제공합니다. 각 항목에는 전반적인 심각도를 나타내는 **점수**&#x200B;가 있어 가장 심각한 취약점의 우선순위를 지정하는 데 도움이 됩니다.

>[!BEGINTABS]

>[!TAB 취약점 세부 정보]

각 취약점에는 [NVD(National Vulnerability Database)](https://nvd.nist.gov/)의 상세 정보로 연결되는 링크가 포함되어 있습니다. 취약성 식별자 또는 설명 오른쪽에 있는 링크 항목을 클릭하면 해당 취약성에 대한 NVD 페이지로 이동합니다.

>[!TAB 항목 무시]

취약점 목록에서 항목을 무시하도록 선택할 수 있습니다. ![삭제 아이콘](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg)을 선택하면 목록에서 항목이 제거됩니다. 무시된 항목은 기회 페이지 상단의 **무시됨** 탭에서 다시 활성화할 수 있습니다.<!---right now it does not seem to be implemented, but the page description mentions this functionality-->

>[!ENDTABS]


## 자동 최적화

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![웹 사이트 취약점 자동 최적화](./assets/website-vulnerabilities/auto-optimize.png){align="center"}

Sites Optimizer Ultimate에는 발견된 취약점에 대해 자동 최적화를 배포하는 기능이 추가됩니다.

>[!BEGINTABS]

>[!TAB 최적화 배포]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 승인 요청]

{{auto-optimize-request-approval}}

>[!ENDTABS]