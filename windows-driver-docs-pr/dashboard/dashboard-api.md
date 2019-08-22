---
title: ハードウェア ダッシュボード API
description: Microsoft ハードウェア API では、組織のパートナー センター アカウント内でハードウェア製品の申請をプログラムで照会したり、作成したりします。
ms.topic: article
ms.date: 09/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e996a8ae33dc4e491eef281398f65e6e31c7a00
ms.sourcegitcommit: 202a9dd161090af3e3815e3fbf3da0bcad993e0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68685593"
---
# <a name="hardware-dashboard-api"></a>ハードウェア ダッシュボード API

組織のパートナー センター アカウント内でハードウェア製品の申請をプログラムで照会したり、作成したりするには、*Microsoft Hardware API* を使用します。 これらの API は、アカウントで多数の製品を管理していて、それらのアセットの申請プロセスを自動化して最適化する必要がある場合に役立ちます。 これらの API は、Azure Active Directory (Azure AD) を使って、アプリまたはサービスからの呼び出しを認証します。
この手順では、Microsoft ハードウェア API を使用した場合のプロセスについて詳しく説明します。

1. これらの API は、ハードウェア [パートナー センター プログラム](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)に参加しているアカウントでのみ使用できます。

2. 下の前提条件を完了したことを確認します。

3. Microsoft ハードウェア API のメソッドを呼び出す前に、Azure AD アクセス トークンを取得する必要があります (下図参照)。 トークンを取得した後、Microsoft Store 申請 API の呼び出しでこのトークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れた後は、新しいトークンを生成できます。

4. Microsoft ハードウェア API を呼び出します。

## <a name="complete-the-prerequisites-for-using-the-microsoft-hardware-api"></a>Microsoft ハードウェア API を使うための前提条件を満たす

Microsoft ハードウェア API を呼び出すコードの作成を開始する前に、次の必須の前提条件を満たしていることを確認します。

* ユーザー (またはユーザーの組織) は、Azure AD ディレクトリと、そのディレクトリに対する[全体管理者](https://go.microsoft.com/fwlink/?LinkId=746654)のアクセス許可を持っている必要があります。 Office 365 または Microsoft の他のビジネス サービスを既に使っている場合は、既に Azure AD ディレクトリをお持ちです。 それ以外の場合は、追加料金なしに[パートナー センターで新しい Azure AD を作成](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-partner-center#create-a-brand-new-azure-ad-to-associate-with-your-partner-center-account)できます。

* Azure AD アプリケーションがまだ存在しない場合は、[それを作成する必要があります](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#create-a-new-azure-ad-application-account-in-your-organizations-directory-and-add-it-to-your-partner-center-account)。

* [Azure AD アプリケーションをパートナー センター アカウントに関連付け](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-partner-center)、**マネージャー** ロールを割り当てる必要があります。

* 自分の [Azure AD アプリケーション テナント ID、クライアント ID、キー](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#manage-keys-for-an-azure-ad-application)を集めます。  **必ずこのキー情報を印刷またはコピーしてください。このキー作成ページを閉じると、この情報にはアクセスできなくなります。** 

## <a name="assigning-the-appropriate-hardware-roles-to-your-azure-ad-application"></a>Azure AD アプリケーションに適切なハードウェア ロールを割り当てる

上記の前提条件を満たしたら、Azure AD アプリケーションで申請および配送先住所ラベルを作成および管理できるように、適切なロールを割り当てる必要があります。

1. パートナー センターで、歯車アイコン (ダッシュボードの右上隅の近く) を選択し、 **[開発者向け設定]** を選択します。 **[設定]** メニューで **[ユーザー]** を選択します。

2. **[ユーザー]** ページで、 **[Azure AD アプリケーション]** を選択し、パートナー センター アカウントの送信へのアクセスに使用するアプリまたはサービスを表す Azure AD アプリケーションを選択します。  

3. このページで、 **[Roles]\(役割\)** の下の **[ハードウェア]** をクリックします。

    ![[役割] セクションの [ハードウェア] タブを示す画像](images/hardware-tab-in-roles-section.png)

    **[Driver Submitter]\(ドライバーの送信者\)** 、 **[Shipping Label owner]\(配送先住所ラベルの所有者\)** 、(使用できる場合は) **[Shipping Label promoter]\(配送先住所ラベルのプロモーター\)** を選択します。  [これらのロールに関する詳細情報](https://docs.microsoft.com/windows-hardware/drivers/dashboard/managing-user-roles)
    

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

次のサンプルは、Microsoft Surface and Devices チームによって作成された完全なエンド ツー エンドの構築済みソリューションと共に Microsoft Hardware API を使用する方法を示す詳細なコードとして利用できます。

* [C# のサンプル](http://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)

[Surface Dev Center Manager ツール (GitHub)](https://github.com/Microsoft/SDCM)

## <a name="additional-help"></a>追加のヘルプ

Microsoft Store 申請 API について質問がある場合や、この API を使った申請の管理に関してサポートが必要な場合は、[サポート ページ](https://partner.microsoft.com/dashboard/account/help?returnUri=https://developer.microsoft.com/dashboard/hardware)にアクセスしてサポートを要求してください。

## <a name="related-topics"></a>関連トピック

[Azure Active Directory とは](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
