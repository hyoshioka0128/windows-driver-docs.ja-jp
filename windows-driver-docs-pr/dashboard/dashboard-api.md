---
title: ハードウェア ダッシュボード API
description: Microsoft ハードウェア API では、組織のパートナー センター アカウント内でハードウェア製品の申請をプログラムで照会したり、作成したりします。
ms.topic: article
ms.date: 09/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c1840caeb7848ce576d2ecb8a23647231ee0524
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518668"
---
# <a name="hardware-dashboard-api"></a>ハードウェア ダッシュボード API

組織のパートナー センター アカウント内でハードウェア製品の申請をプログラムで照会したり、作成したりするには、*Microsoft Hardware API* を使用します。 これらの API は、アカウントで多数の製品を管理していて、それらのアセットの申請プロセスを自動化して最適化する必要がある場合に役立ちます。 これらの API は、Azure Active Directory (Azure AD) を使って、アプリまたはサービスからの呼び出しを認証します。
この手順では、Microsoft ハードウェア API を使用した場合のプロセスについて詳しく説明します。

1. これらの API は、[パートナー センター プログラム](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)に参加している開発者アカウントでのみ使用できます。

2. 下の前提条件を完了したことを確認します。

3. Microsoft ハードウェア API のメソッドを呼び出す前に、Azure AD アクセス トークンを取得する必要があります (下図参照)。 トークンを取得した後、Microsoft Store 申請 API の呼び出しでこのトークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れた後は、新しいトークンを生成できます。

4. Microsoft ハードウェア API を呼び出します。

## <a name="complete-the-prerequisites-for-using-the-microsoft-hardware-api"></a>Microsoft ハードウェア API を使うための前提条件を満たす

Microsoft ハードウェア API を呼び出すコードの作成を開始する前に、次の前提条件が完了していることを確認します。

* ユーザー (またはユーザーの組織) は、Azure AD ディレクトリと、そのディレクトリに対する[全体管理者](https://go.microsoft.com/fwlink/?LinkId=746654)のアクセス許可を持っている必要があります。 Office 365 または Microsoft の他のビジネス サービスを既に使っている場合は、既に Azure AD ディレクトリをお持ちです。 それ以外の場合は、追加料金なしに[パートナー センターで新しい Azure AD を作成](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-dev-center#create-a-brand-new-azure-ad-to-associate-with-your-dev-center-account)できます。

* [Azure AD アプリケーションをパートナー センター アカウントに関連付け](https://docs.microsoft.com/windows/uwp/monetize/create-and-manage-submissions-using-windows-store-services#associate-an-azure-ad-application-with-your-windows-dev-center-account)、テナント ID、クライアント ID、キーを取得する必要があります。 これらの値は、Microsoft ハードウェア API の呼び出しで使用する Azure AD アクセス トークンを取得するために必要です。

## <a name="associate-an-azure-ad-application-with-your-windows-partner-center-account"></a>Azure AD アプリケーションと Windows パートナー センター アカウントの関連付け

Microsoft Hardware API を使うには、事前に Azure AD アプリケーションをパートナー センター アカウントに関連付け、アプリケーションのテナント ID とクライアント ID を取得して、キーを生成しておく必要があります。 Azure AD アプリケーションは、Microsoft ハードウェア API の呼び出し元のアプリまたはサービスを表します。 テナント ID、クライアント ID、およびキーは、API に渡す Azure AD アクセス トークンを取得するために必要です。

1. パートナー センターで、**[アカウント]** 設定に移動して **[ユーザー]** 管理をクリックし、[組織のパートナー センター アカウントを組織の Azure AD ディレクトリに関連付け](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-dev-center)ます。
2. **[ユーザーの管理]** ページで、**[Add Azure AD applications]\(Azure AD アプリケーションの追加\)** をクリックして、パートナー センター アカウントの申請へのアクセスに使うアプリやサービスを表す Azure AD アプリケーションを追加し、**マネージャー** ロールを割り当てます。 このアプリケーションが既に Azure AD ディレクトリに存在する場合、**[Add Azure AD applications]\(Azure AD アプリケーションの追加\)** ページで選んでパートナー センター アカウントに追加できます。 それ以外の場合、**[Azure AD アプリケーションの追加]** ページで新しい Azure AD アプリケーションを作成できます。 詳しくは、「[Add Azure AD applications to your Partner Center account (Azure AD アプリケーションをパートナー センター アカウントに追加する)](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#azure-ad-applications)」をご覧ください。

3. **[ユーザーの管理]** ページに戻り、Azure AD アプリケーションの名前をクリックしてアプリケーション設定に移動し、**[テナント ID]** と **[クライアント ID]** の値を書き留めます。

4. **[新しいキーの追加]** をクリックします。 次の画面で、**[キー]** の値を書き留めます。 このページから離れると、この情報に再度アクセスすることはできません。 詳しくは、「[Azure AD アプリケーションのキーを管理する方法](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#manage-keys)」をご覧ください。

5. 最後に、AD アプリケーションがドライバーの提出を管理し公開するのに必要な役割を持っていることを確認します。 最初に、パートナー センターの **[設定]** パネルで、**[ユーザー]** をクリックします。

    ![[設定] メニューの [ユーザー] オプションを示す画像](images/settings-menu-users-option.png)

    [ユーザー] ページで、**[Azure AD applications]\(Azure AD アプリケーション\)** をクリックします。

    ![[Azure AD アプリケーション] タブを示す画像](images/azure-ad-applications-tab.png)

    関連付けた Azure AD アプリケーションの名前をクリックします。 これにより、Azure AD アプリケーションの詳細ページが読み込まれます。 このページで、**[Roles]\(役割\)** の下の **[ハードウェア]** をクリックします。

    ![[役割] セクションの [ハードウェア] タブを示す画像](images/hardware-tab-in-roles-section.png)

    **[Driver Submitter]\(ドライバーの提出者\)** と **[Shipping Label owner]\(配送先住所ラベルの所有者\)** がオンになっていることを確認します。

    ![[ドライバーの提出者] と [配送先住所ラベルの所有者] チェック ボックスを示す画像](images/driver-submitter-and-shipping-label-owners-checkboxes.png)

## <a name="obtain-an-azure-ad-access-token"></a>Azure AD アクセス トークンの取得

Microsoft ハードウェア API のいずれかのメソッドを呼び出す前に、まず API の各メソッドの **Authorization** ヘッダーに渡す Azure AD アクセス トークンを取得する必要があります。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れた後は、トークンを更新してそれ以降の API 呼び出しで引き続き使用できます。 アクセス トークンを取得するには、「[クライアント資格情報を使用したサービス間の呼び出し](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-service-to-service/)」の手順に従って、HTTP POST を `https://login.microsoftonline.com/<tenant_id>/oauth2/token` エンドポイントに送信します。 要求の例を次に示します。

```cpp
POST https://login.microsoftonline.com/<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8

grant_type=client_credentials
&client_id=<your_client_id>
&client_secret=<your_client_secret>
&resource=https://manage.devcenter.microsoft.com
```

POST URI の *tenant_id* の値と *client_id* および *client_secret* のパラメーターには、前のセクションでパートナー センターから取得したアプリケーションのテナント ID、クライアント ID、キーを指定します。 *resource* パラメーターには、`https://manage.devcenter.microsoft.com` を指定します。

アクセス トークンの有効期限が切れた後は、「[アクセス トークンの更新](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-code/#refreshing-the-access-tokens)」の指示に従ってアクセス トークンを更新できます。

## <a name="use-the-microsoft-hardware-api"></a>Microsoft ハードウェア API の使用

Azure AD アクセス トークンを取得したら、Microsoft ハードウェア API のメソッドを呼び出すことができます。 API には、シナリオにグループ化される多くのメソッドが含まれています。 申請を作成または更新するには、通常、Microsoft ハードウェア API の複数のメソッドを特定の順序で呼び出します。 各シナリオと各メソッドの構文について詳しくは、次の表の記事をご覧ください。

| シナリオ | 説明 |
|:--|:--|
| ドライバー | パートナー センター アカウントに登録されているドライバーを取得、作成、更新します。 これらのメソッドについて詳しくは、次の記事をご覧ください。<ul><li>[製品データを取得する](get-product-data.md)</li><li>[製品申請を管理する](manage-product-submissions.md)</li><li>[配送先住所ラベルのデータを取得する](get-shipping-labels.md)</li><li>[配送先住所ラベルを管理する](manage-shipping-labels.md)</li></ul>|

## <a name="code-examples"></a>コード例

次のサンプルは、Microsoft ハードウェア API を使用する方法を示す詳しいコードを提供します。

* [C# のサンプル](http://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)

## <a name="additional-help"></a>追加のヘルプ

Microsoft Store 申請 API について質問がある場合や、この API を使った申請の管理に関してサポートが必要な場合は、[サポート ページ](https://developer.microsoft.com/dashboard/account/help?returnUri=https://developer.microsoft.com/dashboard/hardware)にアクセスしてサポートを要求してください。
