---
title: Sites Optimizer 설정
description: Sites Optimizer 설정을 구성하고 다른 도구와 통합하는 방법을 알아봅니다.
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: ht
source-wordcount: 749
ht-degree: 100%

---

# Sites Optimizer 설정

![Sites Optimizer 설정](./assets/settings/hero.png){align="center"}

Sites Optimizer 설정들은 Sites Optimizer 경험을 구성하는 중앙 허브입니다.

## Google Search Console

![Google Search Console에 대한 Sites Optimizer 설정](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer의 Google Search Console 설정 커넥터를 사용하면 검색 순위, 클릭스루 비율, Core Web Vitals과 같은 주요 SEO 지표를 분석할 수 있습니다. Google Search Console을 연결하면 JSON 분석을 활용하여 최적화 기회를 발견하고 사이트 성과를 개선할 수 있습니다.

이 커넥터를 설정하려면 해당 도메인의 Google Search Console에 대한 관리자 액세스 권한이 있는 자격 증명이 있어야 합니다.

## AEM Sites에 연결

이 안내서에서는 기존 Edge Delivery Services(EDS) 사이트를 AEM Sites Optimizer에 연결하는 방법을 설명합니다. 시작하기 전에 EDS 사이트가 이미 설정되어 있고 작동 중인지 확인하십시오. 이 연결은 특히 AEM Sites Optimizer가 콘텐츠에 액세스할 수 있도록 하기 위한 작업입니다.

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
   `experience-success-studio@helix-225321.iam.gserviceaccount.com`
3. 권한 수준을 **편집기**&#x200B;로 설정합니다.
4. **사용자에게 알림**&#x200B;을 선택 취소하고 **공유**&#x200B;를 클릭합니다.

공유가 완료되면 대화 상자에서 **연결 유효성 검사**&#x200B;를 클릭한 후 **저장**&#x200B;을 클릭합니다.
