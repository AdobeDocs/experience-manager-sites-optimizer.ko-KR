---
title: CORS 구성 영업 기회 설명서
description: CORS 구성 영업 기회에 대해 알아보고 사이트 보안 취약점을 식별하고 수정합니다.
badgeSecurityPosture: label="보안 태세" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="보안 태세"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---


# CORS 구성 기회

![CORS 구성 기회](./assets/cors-configuration/hero.png){align="center"}

CORS(원본 간 리소스 공유)를 올바르게 구성하는 것은 승인되지 않은 데이터 액세스로부터 웹 애플리케이션을 보호하는 데 필수적입니다. `Access-Control-Allow-Origin` 헤더가 `*`(으)로 설정되면 모든 도메인이 응답을 요청하고 수신할 수 있으므로 중요한 정보가 공격자에게 노출될 수 있습니다. 이는 신뢰할 수 있는 도메인의 제어된 허용 목록을 구현하거나 필요하지 않은 CORS를 비활성화하여 보안을 강화할 수 있는 기회를 제공합니다. 안전한 CORS 설정을 보장하면 승인된 사용자에 대한 원활한 액세스를 유지하면서 개인 컨텐츠를 보호할 수 있습니다.

## 자동 식별

![CORS 구성 기회 자동 식별](./assets/cors-configuration/auto-identify.png){align="center"}

자동 식별은 웹 사이트에서 CORS 잘못된 구성을 검색하고 무단 액세스에 취약한 URL을 검색합니다. 이러한 URL은 다음 세부 정보와 함께 맨 위 표에 나열되어 있습니다.

* **페이지 접두사** - CORS 잘못된 구성에 취약한 URL 경로 접두사입니다.
* **페이지 예제** - 권한 없는 액세스가 가능한 예제 URL.

## 자동 제안

![CORS 구성 자동 제안](./assets/cors-configuration/auto-suggest.png){align="center"}

자동 제안에서는 느슨한 CORS 정책을 설정할 수 있는 검토할 **응용 프로그램 코드 파일** 및 **줄**&#x200B;을 제공합니다.


## [!BADGE Ultimate] 자동 최적화{type=Positive tooltip="Ultimate"}



>[!BEGINTABS]

>[!TAB 최적화 배포]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 승인 요청]

{{auto-optimize-request-approval}}

>[!ENDTABS]
