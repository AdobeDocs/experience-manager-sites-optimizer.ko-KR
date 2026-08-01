---
title: Preflight 감사 실행
description: 페이지에서 Preflight 감사를 시작하는 방법을 알아봅니다.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 17%

---


# Preflight 감사

Preflight는 페이지를 감사하여 게시하기 전에 콘텐츠를 향상할 수 있는 기회를 식별합니다. 자동 스캔과 달리 감사를 실행할 시기를 선택하므로 준비가 되면 언제든지 페이지를 분석할 수 있습니다.

![페이지 분석 단추가 있는 Preflight 랜딩 화면](./assets/audits/hero.png){align="center"}

페이지에 대해 Preflight 감사를 실행하는 방법은 다음과 같습니다.

1. [작성 환경](./access-preflight.md)(범용 편집기, 문서 기반 작성 또는 AEM Sites 페이지 편집기)에서 감사할 페이지를 엽니다.
1. [Preflight 패널](./access-preflight.md)을 엽니다. **성능 준비 감사 실행** 랜딩 화면으로 Preflight가 열립니다.
1. **페이지 분석**&#x200B;을 선택합니다. Preflight는 현재 페이지에서 모든 감사를 실행하고 준비 대시보드를 엽니다. 이 대시보드에는 범주별로 그룹화된 준비 점수와 찾은 기회가 표시됩니다.

미리 보기 결과를 이해하고 최적화 기회를 식별하려면 [Preflight의 결과 감사](./audit-results.md)를 참조하십시오.

## 통합된 Preflight 버튼 사용

작성자 환경에서 [AEM 2026.7.0(릴리스 27083)](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083) 이상을 실행하는 경우 Preflight가 AEM Sites 페이지 편집기 도구 모음에 빌드됩니다. **Preflight** 아이콘(재생 단추)을 선택하여 현재 페이지에 대한 패널을 연 다음 **페이지 분석**&#x200B;을 선택하여 감사를 실행합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3496629?learn=on&enablevpops)

## 이전 세션 계속

Preflight는 가장 최근 실행을 기억하므로 나갔다가 돌아오는 경우 감사를 다시 실행할 필요가 없습니다.

* **동일한 브라우저 탭**&#x200B;에서 [프리플라이트] 패널을 다시 열면 새로 고친 후를 포함하여 [프리플라이트]가 마지막 실행 결과를 자동으로 로드합니다.
* 새 탭에서 **을(를) 반환하거나 브라우저를 닫은 후**&#x200B;을(를) 반환하면 랜딩 화면에 **페이지 분석** 옆에 **마지막 세션 계속** 단추가 표시됩니다. 최근 결과를 다시 로드하려면 **마지막 세션 계속**&#x200B;을 선택하고, 새 실행을 시작하려면 **페이지 분석**&#x200B;을 선택하십시오.

Preflight는 각 페이지에 대해 가장 최근 실행을 개별적으로 추적하므로 **마지막 세션 계속**&#x200B;은(는) 항상 현재 사용 중인 페이지에 대한 마지막 실행을 다시 로드합니다.

감사가 완료되고 결과가 표시되면 **추가 작업**(**...**)에서 **다시 분석**&#x200B;을 선택합니다. 결과를 무시하고 모든 감사를 다시 실행할 수 있는 도구 모음의 메뉴 [Preflight의 감사 결과](./audit-results.md#toolbar)를 참조하십시오.

