---
title: Sites Optimizer 설정
description: Sites Optimizer 설정을 구성하고 다른 도구와 통합하는 방법을 알아봅니다.
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
source-git-commit: 37d90154e6868ee392bf1b779b2bf3697112b7ce
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 39%
---
# Sites Optimizer 설정

![Sites Optimizer 설정](./assets/settings/hero.png){align="center"}

Sites Optimizer 설정들은 Sites Optimizer 경험을 구성하는 중앙 허브입니다.

## Google Search Console

![Google Search Console에 대한 Sites Optimizer 설정](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer의 Google Search Console 설정 커넥터를 사용하면 검색 순위, 클릭스루 비율, Core Web Vitals과 같은 주요 SEO 지표를 분석할 수 있습니다. Google Search Console을 연결하면 JSON 분석을 활용하여 최적화 기회를 발견하고 사이트 성능을 개선할 수 있습니다.

이 커넥터를 설정하려면 해당 도메인의 Google Search Console에 대한 관리자 액세스 권한이 있는 자격 증명이 있어야 합니다.

## AEM Sites에 연결

이 안내서에서는 기존 Edge Delivery Services(EDS) 사이트를 AEM Sites Optimizer에 연결하는 방법을 설명합니다. 시작하기 전에 EDS 사이트가 이미 설정되어 있고 작동 중인지 확인하십시오. 이 연결은 AEM Sites Optimizer가 콘텐츠에 액세스할 수 있도록 특별히 마련된 것입니다.

이 연결 작업을 수행하려면 다음과 같은 두 가지 단계를 거쳐야 합니다.

1. 코드 저장소 URL과 콘텐츠 소스 URL을 제공합니다.
2. AEM Sites Optimizer에 콘텐츠 소스에 대한 액세스 권한을 부여합니다.

### 1단계 — 코드 저장소와 콘텐츠 소스 연결

AEM Sites Optimizer에서 **설정 → AEM Sites에 연결**&#x200B;로 이동하여 다음을 입력합니다.

- **코드 저장소 URL** — EDS 사이트의 GitHub URL(예:
  `https://github.com/owner/repo`

- **콘텐츠 소스 URL** — EDS 사이트를 지원하는 SharePoint 폴더 또는 Google Drive 폴더의 URL(예:
  `https://drive.google.com/drive/folders/...` 또는 `https://myorg.sharepoint.com/...`

콘텐츠 소스 URL을 입력하면 AEM Sites Optimizer에서 콘텐츠 소스 유형을 감지하고 아래에 관련 액세스 지침을 표시합니다.

### 2단계 — 콘텐츠 소스에 대한 액세스 권한 부여

콘텐츠 소스와 일치하는 섹션을 따릅니다.

#### SharePoint — Adobe 도메인

![Adobe SharePoint 도메인에 대해 작업이 필요하지 않음을 보여 주는 AEM Sites에 연결 대화 상자](./assets/settings/connect-content-and-drive.png){align="center"}

콘텐츠 소스 URL에 Adobe SharePoint 도메인을 사용하는 경우 추가 작업이 필요하지 않습니다. 액세스는 이미 구성되어 있습니다. **저장**&#x200B;을 클릭하여 연결을 완료합니다.

#### SharePoint — 사용자 정의 도메인

콘텐츠 소스 URL에 조직의 자체 SharePoint 도메인을 사용하는 경우 Azure 애플리케이션을 등록하고 AEM Sites Optimizer에 해당 자격 증명을 제공해야 합니다.

##### 필요 사항

- Azure Portal에서 애플리케이션을 등록할 수 있는 권한 또는 사용자를 대신하여 애플리케이션을 등록할 수 있는 담당자
- API 동의를 부여할 수 있는 테넌트 관리자 권한 또는 사용자를 대신하여 API 동의를 승인할 수 있는 관리자

##### 2a 단계 — Azure에서 애플리케이션 등록

1. **Azure Portal → Microsoft Entra ID → 앱 등록 → 새 등록**&#x200B;으로 이동합니다.
2. 애플리케이션 이름을 지정합니다(예: `AEM Sites Optimizer`).
3. 다른 모든 기본값을 그대로 두고 **등록**&#x200B;을 클릭합니다.
4. **개요** 페이지에서 다음 항목을 기록합니다.
   - **애플리케이션(클라이언트) ID**
   - **디렉터리(테넌트) ID**

##### 2b 단계 — API 권한 추가

1. **API 권한 → 권한 추가 → Microsoft Graph → 애플리케이션 권한**&#x200B;으로 이동합니다.
2. 다음 두 가지 항목을 모두 추가합니다.
   - `Sites.Selected` — 특정 SharePoint 사이트 컬렉션에 대한 범위가 지정된 액세스
   - `Files.SelectedOperations.Selected` — 로그인한 사용자 없이 파일 액세스
3. 두 항목에 대해 **관리자 동의 부여**&#x200B;를 클릭합니다.

![Sites.Selected 및 Files.SelectedOperations.Selected 권한이 부여되었음을 보여 주는 Azure API 권한](./assets/settings/app-permissions.png){align="center"}

>[!NOTE]
>
>관리자 동의를 부여하려면 테넌트 관리자 권한이 필요합니다. 해당 권한이 없는 경우 계속 진행하기 전에 IT 또는 Azure 관리자에게 이 단계를 완료하도록 요청하십시오.

##### 2c 단계 — 클라이언트 암호 만들기

![앱 등록을 위한 Azure 인증서 및 암호 페이지](./assets/settings/create-credentials.png){align="center"}

1. **인증서 및 암호 → 새 클라이언트 암호**&#x200B;로 이동합니다.
2. 설명과 만료를 설정한 후 **추가**&#x200B;를 클릭합니다.
3. 암호 값을 즉시 복사합니다. 암호 값은 한 번만 표시됩니다.

##### 2d 단계 — 앱에 SharePoint 사이트에 대한 액세스 권한을 부여합니다.

Microsoft Graph Explorer, PowerShell 또는 직접 Graph API 호출을 사용하여 앱에 액세스 권한을 부여할 수 있습니다.

[Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)로 이동하여 Microsoft 계정으로 로그인하고 다음 요청을 실행합니다.

1. 사이트 ID를 찾습니다.

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. 응답에서 `id`를 복사한 후 사이트 수준 액세스 권한을 부여합니다.

```
POST https://graph.microsoft.com/v1.0/sites/{siteId}/permissions
```

본문:

```json
{
  "roles": ["write"],
  "grantedToIdentities": [{
    "application": {
      "id": "{your-client-id}",
      "displayName": "{Your app name}"
    }
  }]
}
```

##### 2e 단계 — AEM Sites Optimizer에서 자격 증명 입력

![SharePoint 자격 증명 필드를 보여 주는 AEM Sites에 연결 대화 상자](./assets/settings/add-sharepoint-credentials.png){align="center"}

**AEM Sites에 연결** 대화 상자로 돌아가서 **SharePoint를 통한 콘텐츠 저장소 연결**&#x200B;에 다음 항목을 입력합니다.

- **테넌트 ID(Azure AD)** — 앱 등록 → 개요
- **클라이언트 ID(앱 등록)** — 앱 등록 → 개요
- **클라이언트 암호** — 2c 단계에서 생성됨

**연결 유효성 검사**&#x200B;를 클릭하여 액세스를 확인한 후 **저장**&#x200B;을 클릭합니다.

#### Google Drive

![액세스 공유를 위한 Google Drive 서비스 계정을 보여 주는 AEM Sites에 연결 대화 상자](./assets/settings/validate-eds-google.png){align="center"}

1. Google Drive에서 EDS 사이트를 지원하는 폴더를 마우스 오른쪽 버튼으로 클릭하고 **공유**&#x200B;를 선택합니다.
2. **사용자 및 그룹 추가** 필드에 **AEM Sites에 연결** 대화 상자에 표시된 서비스 계정 이메일을 입력합니다.
   `aem-sites-optimizer@adbe-gcp0843.iam.gserviceaccount.com`
3. 권한 수준을 **편집기**&#x200B;로 설정합니다.
4. **사용자에게 알림**&#x200B;을 선택 취소하고 **공유**&#x200B;를 클릭합니다.

공유가 완료되면 대화 상자에서 **연결 유효성 검사**&#x200B;를 클릭한 후 **저장**&#x200B;을 클릭합니다.

## 사용자 권한 관리

Sites Optimizer에서 사이트에 액세스할 수 있는 사용자와 이를 사용하여 수행할 수 있는 작업을 제어합니다. 액세스 권한은 각 사용자에게 부여하는 독립적인 *기능*(보기, 편집, 배포, 구성 및 사용자 관리)의 작은 집합에서 만들어집니다.

액세스 권한은 **additive**&#x200B;입니다. 개인의 권한은 부여된 모든 것의 합계입니다. 거부가 없기 때문에 지원금은 서로 충돌하거나 취소하지 않습니다. 다른 사용자에게 더 적은 액세스 권한을 부여하려면 권한 부여를 무시하지 말고 제거하십시오.

### 액세스 권한 부여 방법

사용자가 액세스할 수 있는 방법에는 두 가지가 있으며 함께 작동합니다.

- **조직 전체 액세스** — [Adobe Admin Console](https://adminconsole.adobe.com/)에서 Adobe 조직 관리자가 할당했습니다. 조직의 모든 사이트에 적용됩니다. 모든 곳에서 동일한 액세스를 필요로 하는 사람들을 위해 사용하십시오.
- **사이트 수준 액세스** — **권한 설정** 페이지에서 Sites Optimizer →에 할당되었습니다. 단일 사이트에 적용되며 필요한 만큼 광범위하거나 좁을 수 있습니다. Admin Console 액세스가 필요하지 않습니다.

>[!NOTE]
>
>두 개의 레이어가 더해집니다. 한 사이트에서 편집 권한이 부여된 조직 전체 보기 액세스 권한을 가진 사용자는 모든 사이트를 보고 해당 사이트를 편집할 수 있습니다. 한 사람을 단일 사이트로 제한하려면 이들이 조직 전체의 역할도 담당하지 않도록 해야 합니다.

#### 조직 전체 역할(Admin Console)

조직 전체 액세스는 [AEM Sites Optimizer](https://adminconsole.adobe.com/)에서 할당된 두 **Adobe Admin Console** 제품 역할 중 하나에서 가져옵니다.

- **ASO 관리자** — **사용자 관리**&#x200B;를 포함하여 모든 사이트에 대한 전체 액세스 권한. 관리자는 모든 사이트에 대한 **권한** 페이지를 열고 다른 사용자에게 액세스 권한을 할당할 수 있습니다.
- **ASO 사용자** — 모든 사이트에 대한 보기 전용 액세스 권한. 변경 사항 및 사용자 관리 없음.

역할을 할당하려면 조직의 **시스템 관리자** 또는 AEM Sites Optimizer의 **제품 관리자**&#x200B;여야 합니다.

1. [Adobe Admin Console](https://adminconsole.adobe.com/)에 로그인합니다.
1. **제품**(으)로 이동하여 **AEM Sites Optimizer**&#x200B;을(를) 선택하십시오.
1. **사용자** 탭을 열고 전자 메일로 사용자를 추가합니다(또는 기존 사용자를 선택).
1. **+**(추가) 아이콘을 클릭하여 제품 프로필을 추가한 다음 제품 프로필을 선택합니다.

   ![Adobe Admin Console에서 사용자에 대한 제품 프로필 선택](./assets/settings/permissions-admin-console-product-profile.png){align="center"}

1. **다음**&#x200B;을 클릭합니다.
1. 역할(전체 액세스용 **ASO 관리자** 또는 보기 전용 액세스용 **ASO 사용자**)을 선택한 다음 **적용**&#x200B;을 클릭합니다.

   ![Adobe Admin Console에서 ASO 관리자 역할 선택](./assets/settings/permissions-admin-console-aso-manager-role.png){align="center"}

   ![Adobe Admin Console에서 ASO 사용자 역할 선택](./assets/settings/permissions-admin-console-aso-user-role.png){align="center"}

사용자 추가에 대한 자세한 내용은 [사용자 온보딩](setup/onboard-users.md)을 참조하십시오.

>[!IMPORTANT]
>
>조직 관리자만 조직 전체에 **사용자 관리**&#x200B;를 부여할 수 있습니다. 사이트에 **사용자 관리**&#x200B;가 있는 구성원은 해당 사이트에 대한 액세스 권한을 할당할 수 있지만 조직 전체의 **ASO 관리자**&#x200B;를 만들 수는 없습니다.

### 기능 수준

각 기능은 한 가지 종류의 작업을 제어합니다. 이러한 속성은 독립적입니다. 예를 들어 편집 없이 배포를 허용할 수 있습니다.

| 기능 | 허용 사항 | 허용되지 않는 사항 |
|---|---|---|
| 보기 | 아무 것도 변경하지 않고 사이트의 데이터(기회, 제안, 수정 사항, 보고서 및 구성)를 확인합니다. | 모든 변경 사항 |
| 편집 | 영업 기회와 제안 사항을 만들고 변경합니다(변경 사항). | 변경 사항 게시, 설정 변경 또는 사용자 관리 |
| 배포 | 수정 사항을 사이트에 실시간으로 게시하고 롤백합니다. | 사용자 관리. |
| 구성 | 사이트의 설정 및 연결을 변경합니다. | 수정 사항 게시 또는 사용자 관리 |
| 사용자 관리 | 다른 구성원의 사이트 액세스 권한을 부여하거나 취소합니다. | 개인이 아직 액세스할 수 없는 사이트 관리 |

>[!NOTE]
>
>**보기가 항상 포함됩니다.** 모든 부여에는 자동으로 보기가 포함됩니다. 볼 수 없는 항목을 관리, 구성, 편집 또는 배포할 수 없습니다. 이로 인해 보기는 자체적으로 제거할 수 없습니다. 다른 사람의 액세스 권한을 완전히 제거하려면 모든 기능을 선택 취소하는 대신 해당 구성원을 제거합니다(아래 [구성원 편집 또는 제거](#edit-or-remove-a-member) 참조).

### 영업 기회 유형에 대한 액세스 범위 지정

단일 사이트에서 전체 사이트 대신 **특정 영업 기회 유형**(예: Core Web Vitals 또는 끊어진 내부 링크)에 대한 보기, 편집 및 배포를 허용할 수 있습니다. 이렇게 하면 한 사람이 다른 모든 항목을 보면서 Core Web Vitals을 편집할 수 있습니다.

- **보기**, **편집** 및 **배포**&#x200B;의 범위를 하나 이상의 영업 기회 형식 또는 **모두**&#x200B;개의 영업 기회 형식으로 지정할 수 있습니다.
- **구성** 및 **사용자 관리**&#x200B;은(는) 항상 전체 사이트에 적용됩니다. 영업 기회 유형으로 제한될 수 없습니다.

범위가 지정된 각 부여는 멤버의 고유한 행으로 표시되며 **적용 대상** 열은 영업 기회 유형, **모두** 또는 **사이트 전체**&#x200B;를 표시합니다.

>[!CAUTION]
>
>범위 지정은 *해당* 부여에서 제공하는 권한만 제한합니다. 다른 부여에서 제공하는 액세스 권한은 제거하지 않습니다. 또한 사용자에게 조직 전체 액세스 권한 또는 **모두** 형식의 부여가 있는 경우 더 광범위한 액세스 권한이 적용됩니다. 따라서 특정 영업 기회 유형으로 사용자를 진정으로 제한하려면 더 광범위한 역할 또는 **모두** 유형 부여를 보유하고 있지 않은지 확인하십시오.

### 구성원 추가

1. **사용 권한 설정 →**(으)로 이동하여 사이트를 선택하십시오.
1. **구성원 추가**&#x200B;를 클릭합니다.
1. 이름 또는 전자 메일로 검색하고 한 명 이상의 사용자를 선택합니다.
1. 액세스가 적용되는 **영업 기회 유형**(또는 **모두**)을 선택한 다음 부여할 기능을 선택하십시오.
1. **추가**&#x200B;를 클릭합니다.

<!-- MEDIA PENDING: Site Manager / Site User walkthrough videos are being re-recorded with demo data to remove PII, then re-uploaded to video.tv.adobe.com and embedded here with >[!VIDEO]. The earlier uploads v/3503767 and v/3503768 (KT-22672 / KT-22673) contain PII and must not be used. -->

### 멤버 편집 또는 제거

**구성원** 테이블에서:

- 구성원 행에서 **기능 편집**&#x200B;을 클릭하여 수행할 수 있는 작업을 변경합니다. 기존 부여를 편집할 때 해당 영업 기회 유형은 고정된 상태를 유지합니다. 즉, 기능만 변경하고 하나 이상의 기능은 선택된 상태로 유지되어야 합니다.
- **제거**&#x200B;를 클릭하여 해당 구성원의 사이트 액세스를 완전히 취소하세요.

>[!NOTE]
>
>기능 변경과 멤버 제거는 서로 다른 작업입니다. 모든 액세스 권한을 제거하려면 **제거**&#x200B;를 사용하십시오. 권한 부여에 하나 이상의 기능이 유지되어야 하고 보기가 항상 유지되므로 기능을 선택 취소하면 수행할 수 없습니다.

### 권한을 관리할 수 있는 사람

사이트에 대한 **권한** 페이지는 다음 위치에서 사용할 수 있습니다.

- 해당 사이트에서 **사용자 관리** 기능을 가진 구성원 및
- 조직 관리자(ASO 관리자).

**사용자 관리**&#x200B;가 없는 구성원은 해당 사이트에 대한 액세스 관리 권한이 없다는 메시지를 볼 수 있습니다.

### 사용자 및 액세스 관리 켜기

사용자 및 액세스 관리는 조직의 설정에 의해 제어됩니다. 이 기능을 사용하기 전에 액세스 권한을 할당할 수 있지만 설정이 설정된 후에만 **강제**&#x200B;됩니다.

아직 활성화되지 않은 경우 **권한** 페이지에 계정 팀에 문의하라는 배너가 표시됩니다. Sites Optimizer 계정 팀에 문의하여 이 기능을 켜십시오.

>[!NOTE]
>
>사용자 및 액세스 관리가 켜질 때까지 할당한 권한은 저장되지만 강제 적용되지는 않습니다.

### 자주 묻는 질문

**사이트 수준 구성원이 Admin Console 역할이 필요합니까?**

아니요. 사이트 수준 액세스 권한은 **권한** 페이지의 Sites Optimizer 내에서 전체적으로 부여됩니다. Admin Console에서는 조직 전체 역할만 할당됩니다.

**조직 전체 액세스 권한과 사이트 수준 액세스 권한이 모두 있는 사람은 어떻게 됩니까?**

둘 다 적용됩니다. 그들의 효과적인 접근은 그 둘의 결합이다. 어떤 권한도 액세스를 거부할 수 없으므로 권한은 충돌하지 않습니다.

**사용자 관리 구성원이 조직 전체의 관리자를 만들 수 없는 이유는 무엇입니까?**

조직 전체 역할을 만드는 것은 Admin Console 작업입니다. **사용자 관리**&#x200B;가 있는 구성원은 자신의 사이트에서 액세스 권한을 할당할 수 있지만 조직 관리자만 조직 전체 역할을 부여할 수 있습니다.

**사이트에 대한 사용자의 액세스를 취소하려면 어떻게 해야 합니까?**

**권한** 페이지에서 권한을 제거하십시오. 이는 편집 기능과 다르며, 편집 기능은 항상 하나 이상의 기능을 남겨야 합니다.

**개인을 특정 영업 기회 유형으로 제한할 수 있습니까?**

예 — **모두** 대신 특정 영업 기회 유형에 대한 보기, 편집 또는 배포 권한을 부여합니다. 액세스는 추가적이므로 이 기능은 개인이 조직 전체 액세스 권한이나 **모두** 유형의 부여를 받지 않는 경우에만 적용됩니다.
