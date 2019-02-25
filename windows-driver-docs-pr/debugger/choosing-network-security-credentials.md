---
title: ネットワーク セキュリティ資格情報を選択します。
description: ネットワーク セキュリティ資格情報を選択します。
ms.assetid: f53bda2b-a5e7-4a8e-ac31-44c92f306b7a
keywords:
- SymProxy、ネットワーク セキュリティ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f754585f5b4b561d83cbb36d2bc2cc73b6f9730c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531418"
---
# <a name="choosing-network-security-credentials"></a>ネットワーク セキュリティ資格情報を選択します。


シンボルのプロキシ サーバーは、シンボル ストアを使用して行うをアクセスの適切な特権を持つセキュリティ コンテキストから実行する必要があります。 など、外部の Web ストアからシンボルを取得する場合 https://msdl.microsoft.com/download/symbolsシンボルのプロキシ サーバーのファイアウォールの外部から Web にアクセスする必要があります。 ネットワーク上の他のコンピューターからファイルを取得する場合、シンボルのプロキシ サーバーは、これらの場所からファイルを読み取る適切な特権が必要です。 2 つの可能な選択肢はで、認証にシンボルのプロキシ サーバーを設定するのには、**ネットワーク サービス**アカウントまたはその他のユーザー アカウントと一緒に Directory Domain Services のアクティブな内で管理されているユーザー アカウントを作成します。

**注**  ファイルを読み取るし、c: にコピーするために必要なものだけにするには、このアカウントの特権を制限することをお勧め\\symstore します。 この制限には、システムの破損からの HTTP ストアにアクセスするクライアントができないようにします。

 

**注**  環境内では、ここに表示されるオプションの意味を確認します。 さまざまな組織では、さまざまなセキュリティ ニーズと要件があります。 組織のセキュリティ要件をサポートするためには、こちらのプロセスを変更します。

 

### <a name="span-idauthenticateasanetworkservicespanspan-idauthenticateasanetworkservicespanauthenticate-as-a-network-service"></a><span id="authenticate_as_a_network_service"></span><span id="AUTHENTICATE_AS_A_NETWORK_SERVICE"></span>ネットワーク サービスとして認証します。

**ネットワーク サービス**アカウントが新しいアカウントを作成する手順はありませんので、Windows に組み込まれています。 この例では、シンボルのプロキシ サーバーが構成されているコンピューターを名前*SymMachineName*という名前のドメインで*corp*します。

このコンピューターを許可するのには、外部シンボル ストアまたはインターネット プロキシを構成する必要があります**ネットワーク サービス**アカウント (コンピューター アカウント)、正常に認証します。 これを実現するために 2 つの方法はあります。

-   アクセスできるように、 **Authenticated Users**外部ストアまたはインターネット プロキシ上でグループ化します。

-   コンピューター アカウントにアクセスできるように*corp\\SymMachineName$* します。 シンボルのプロキシ サーバーの「ネットワーク サービス」のアカウントだけへのアクセスを制限するため、このオプションは安全です。

### <a name="span-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanauthenticate-as-a-domain-user"></a><span id="Authenticate_as_a_Domain_User"></span><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>ドメイン ユーザーとして認証します。

この例では、ものとユーザー アカウントの名前は*SymProxyUser*という名前のドメインで*corp*します。

**ユーザー アカウントを IIS に追加する\_ユーザー, ログオフ グループ**

1.  **管理ツール**開く**コンピュータの管理**します。

2.  展開**ローカル ユーザーとグループ**します。

3.  **[グループ]** をクリックします。

4.  ダブルクリック**IIS\_ユーザー, ログオフ**クリックし、中央のウィンドウで**プロパティ**します。

5.  で、**メンバー**セクションで、**追加**します。

6.  型*corp\\SymProxyUser*というラベルの付いたウィンドウで**を選択するオブジェクト名を入力**します。

7.  終了する、 **ユーザー、コンピューター、またはグループ**ダイアログ ボックスで、をクリックして**OK**。

8.  終了する**IIS\_ユーザー, ログオフ プロパティ**、 をクリックして**OK**します。

9.  閉じる、**コンピュータの管理**コンソール。

**アカウントを使用する IIS を設定します。**

1.  **管理ツール**開く**インターネット インフォメーション サービス (IIS) マネージャー**します。

2.  展開**Websites**します。

3.  右クリックして**既定の Web サイト**選択**プロパティ**します。

4.  をクリックして、**ディレクトリ セキュリティ**タブ。

5.  **認証とアクセス制御**セクションで、**を編集しています.**.

6.  確認します*への匿名アクセスを有効にする*がチェックされます。

7.  リモート シンボル サーバー ストアにアクセスする権限を持つアカウントの資格情報を入力します ("corp\\SymProxyUser")、順にクリックします**OK**します。

8.  求められたら、パスワードを再入力し、をクリックして**OK**します。

9.  終了する**Web サイトのプロパティの既定の**、 をクリックして**OK**します。

10. 表示されます、*継承/優先*ダイアログ。 そうである場合にこれを用意する仮想ディレクトリの適用を選択します。

### <a name="span-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanauthenticate-as-a-domain-user-using-the-iiswpg-group"></a><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>IIS を使用してドメイン ユーザーとして認証\_WPG グループ

この例では、ユーザー アカウントの名前は*SymProxyUser*という名前のドメインで*corp*します。 このユーザー アカウントを認証するために追加する必要があります、 **IIS\_WPG**グループ。

**ユーザー アカウントを IIS に追加する\_WPG グループ**

1.  **管理ツール**開く**コンピュータの管理**します。

2.  展開**ローカル ユーザーとグループ**します。

3.  **[グループ]** をクリックします。

4.  ダブルクリック**IIS\_WPG**右側のペインでします。

5.  **[追加]** をクリックします。

6.  型*corp\\SymProxyUser*というラベルの付いたウィンドウで**を選択するオブジェクト名を入力**します。

7.  終了する、 **ユーザー、コンピューター、またはグループ**ダイアログ ボックスで、をクリックして**OK**。

8.  終了する**IIS\_WPG プロパティ**、 をクリックして**OK**します。

9.  閉じる、**コンピュータの管理**コンソール。

 

 





