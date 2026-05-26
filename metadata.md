---
solution: Experience Manager
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
product: adobe experience manager
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
type: Documentation
description: AEM Sites Optimizer 설명서입니다.
index: true
git-repo: https://github.com/AdobeDocs/experience-manager-sites-optimizer.en
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: b6745249d9a773ce875f421dd16947a1a4d0a245
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 2%

---


# 내부 사용을 위한 메타데이터

GitHub 제작 시스템은 다음과 같이 증가하는 선례 수준을 사용하여 메타데이터를 계층적으로 구성합니다.

1. metadata.md
1. 종료 날짜
1. 문서

metadata.md 파일에 정의된 메타데이터는 전체 리포지토리에 적용되지만 ToC 및 문서 수준에서 재정의될 수 있습니다. 메타데이터 재정의는 가능한 한 낮은 수준에서 수행해야 합니다.

`experience-manager-cloud-service.en` 저장소의 메타데이터는 필요한 최소값입니다.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

Tocs

* `sub-product`
* `user-guide-title`

문서

* `title`
* `description`
* `contentOwner`(`/help/assets` 아래의 핵심 자산 콘텐츠에서만)

