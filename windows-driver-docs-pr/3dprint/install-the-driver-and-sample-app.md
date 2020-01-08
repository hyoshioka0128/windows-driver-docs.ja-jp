---
title: ドライバーとサンプル アプリのインストール
description: ここでは、ドライバーと WSD サンプルアプリのインストールについて説明します。
ms.assetid: BF89F0D0-2ED3-4900-996F-BB7B9C8C9B80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68294935d0f139e4faeecd5559c7e23e475b41a8
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652778"
---
# <a name="install-the-driver-and-sample-app"></a>ドライバーとサンプル アプリのインストール


ここでは、ドライバーと WSD サンプルアプリのインストールについて説明します。

## <a name="install-the-driver-on-a-windows81-machine"></a>Windows 8.1 コンピューターにドライバーをインストールする


3D 印刷 SDK に含まれている印刷ドライバーをインストールするには、ドライバーの .inf ファイルを選択し、ファイルを右クリックして、 **[インストール]** を選択します。

## <a name="install-the-sample-app"></a>サンプルアプリをインストールする


最初に Microsoft Visual Studio 2013 (Professional または Ultimate) をインストールし、必要なサービスパックまたは更新プログラムを適用します。

このサンプルの実装は、ASP.NET で実装された Microsoft インターネットインフォメーションサービス (IIS) web サービスで構成されており、http ハンドラーを使用して WS 印刷プロトコル要求に応答します。

ダイレクト検出は、UDP 検出を使用せずに http プロトコルから動作するため、実行中の web サービスで動作できます。

### <a name="installation-requirements"></a>インストール要件

Windows コンピューターに web サービスを展開するには、Microsoft .NET 4.5 と共に、コンピューターに IIS と ASP.NET がインストールされている必要があります。

### <a name="install-iis"></a>IIS のインストール

1.  IIS をインストールするには、 **Windows** + **R**キーの組み合わせを押して **[実行]** ダイアログボックスを開き、「`appwiz.cpl`」と入力し、 **enter**キーを押します。

    ![実行](images/wsd-app-1.png)

    コントロールパネルの **[プログラムと機能]** が開きます。

2.  **コントロールパネル**の ホーム ウィンドウで、 **Windows の機能の有効化または無効化** をクリックします。

    ![プログラムと機能](images/wsd-app-2.png)

3.  **[Windows の機能]** ダイアログボックスで、 **[インターネットインフォメーションサービス]** チェックボックスをオンにします。

    ![Windows の機能](images/wsd-app-3.png)

4.  **[インターネットインフォメーションサービス]** チェックボックスを展開し、 **[World Wide Web Services]** を展開します。

    ![world wide web サービス](images/wsd-app-4.png)

5.  **[アプリケーション開発機能]** を展開し、次に示すサブ機能を選択します。

    ![アプリケーション開発機能](images/wsd-app-5.png)

6.  **[OK]** をクリックします。 **[変更の適用]** ダイアログに、インストールの進行状況が表示されます。

    ![変更の適用](images/wsd-app-6.png)

7.  **[変更の適用]** ダイアログが閉じたら、ブラウザーを開いて https://localhost に移動します。

    ![localhost](images/wsd-app-7.png)

### <a name="publish-the-project"></a>プロジェクトの発行

ハンドラープロジェクトを localhost に発行して、web サービスをデプロイします。

![web の発行](images/wsd-app-8.png)

発行が成功すると、 https://localhost を参照すると、空のファイルが返送されます。 ハンドラーが正しくセットアップされていない場合は、エラーメッセージが表示されるか、既定の IIS web ページが表示される可能性があります。

**DefaultAppPool**を**NetworkService** id で実行するように切り替えると、正常に動作し続けます。 **DefaultAppPool**はネットワーク全体でも機能する必要があります。

### <a name="verify-site-bindings"></a>サイトバインドの検証

IPv6 をサポートする必要がある場合は、ASP.NET サイトバインドが IPv6 用に作成されていることを確認します。

ハンドラープロジェクトは、プロジェクトを**既定の Web サイト**に発行します。

既定では、サイトはすべての IP アドレスのポート80にバインドされています。

![サイトバインド](images/wsd-app-9.png)

### <a name="update-windows-firewall"></a>Windows ファイアウォールの更新

既定では、Windows によってコンピューター上のポート80がブロックされるため、World Wide Web サービス (http) トラフィックを受信できるように Windows ファイアウォールを更新する必要があります。 これをオンにしないと、クライアントからの受信 http 要求は失敗します。

![Windows ファイアウォール](images/wsd-app-10.png)

### <a name="install-the-fabrikam-printer"></a>Fabrikam プリンターをインストールする

### <a name="directed-discovery-via-http-endpoint"></a>Http エンドポイントを介したダイレクト検出

1.  **コントロールパネル**の **[デバイスとプリンター]** を開きます。

2.  **[プリンターの追加]** を選択します。

3.  **目的のプリンターが表示されていない**ことを選択します。

    ![プリンターの追加](images/wsd-app-11.png)

4.  [ **Tcp/ip アドレスまたはホスト名を使用してプリンターを追加**する] を選択します。

    ![他のオプションでプリンターを検索する](images/wsd-app-12.png)

5.  **[デバイスの種類]** の一覧から **[Web サービスデバイス]** を選択します。

    ![デバイスの種類の選択](images/wsd-app-13.png)

6.  ホスト名または IP アドレスを入力し、 **[次へ]** をクリックします。

    **プリンターに接続し**ています... 進行状況バーが表示されます。

    ![ホスト名または ip アドレスを入力してください](images/wsd-app-14.png)

    Fabrikam プリンターがインストールされると、次のメッセージが表示されます。

    ![fabrikam 3d プリンターがインストールされました](images/wsd-app-15.png)

### <a name="ad-hoc-discovery-via-udp-multicast"></a>UDP マルチキャストを使用したアドホック検出

アドホック検出は、ポート3702で探索イベントをリッスンする UDP サーバーを実装することによって実行できます。

交換シーケンスの詳細については、「[検出とメタデータ交換のメッセージパターン](https://docs.microsoft.com/windows/desktop/WsdApi/discovery-and-metadata-exchange-message-patterns)」を参照してください。

 

 




