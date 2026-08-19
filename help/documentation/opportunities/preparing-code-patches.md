---
title: 코드 패치 준비 설명서
description: AEM Sites Optimizer에서 Core Web Vitals 수정을 위해 코드 패치를 준비하는 방법과 이후에 추적하는 방법에 대해 알아봅니다.
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: a86d83ee226055e6401b13fd421b40d449b96fa8
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 2%

---

# 코드 패치 준비 설명서

<!--![Preparing code patches](./assets/preparing-code-patches/hero.png){align="center"}-->

[핵심 웹 바이탈 기회](/help/documentation/opportunities/core-web-vitals.md)에 대해 AEM Sites Optimizer은 식별된 성능 문제에 대한 코드 수준 수정 사항을 생성합니다. 이러한 수정 사항을 직접 배포하지 않고 코드 패치로 검토하고 준비합니다.

## 코드 패치 준비

Core Web Vitals 목록에서 하나 이상의 문제를 선택한 다음 **코드 패치 준비**&#x200B;를 클릭하여 선택 항목을 준비하거나 **모든 코드 패치 준비**&#x200B;를 클릭하여 사용 가능한 모든 패치를 한 번에 준비합니다. AEM Sites Optimizer은 각 수정 사항에 대해 레이블이 지정된 GitHub 문제를 만들고 팀이 검토, 테스트 및 병합할 수 있도록 코드 변경이 있는 연결된 가져오기 요청을 자동으로 엽니다.

코드 패치를 준비할 권한이 없거나, 코드 저장소가 연결되어 있지 않거나, 패치 생성이 아직 진행 중인 경우와 같이 사이트가 코드 패치에 대해 완전히 구성되지 않은 경우에는 이 작업이 비활성화됩니다. 각 경우에 Sites Optimizer에서는 비활성화된 단추 옆에 있는 이유를 설명합니다.

## 준비된 코드 패치 추적

코드 패치를 준비한 후에는 **현재** 및 **무시됨** 탭과 함께 Core Web Vitals 세부 정보 페이지의 **배포됨** 탭에서 관리하고 다음 단계를 수행할 수 있습니다. 패치의 상태는 해당 끌어오기 요청이 생성되었을 뿐만 아니라 병합되었는지 여부를 반영합니다. 수정 사항이 실제로 코드 베이스에 병합되면 문제가 **배포됨**(으)로 이동됩니다.

## 추가 리소스

* [Core Web Vitals 기회](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [작성자 설명서에 배포](/help/documentation/opportunities/deploying-to-author.md)
