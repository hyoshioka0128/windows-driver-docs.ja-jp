---
title: ドライバーとサンプル アプリをインストールします。
description: このセクションでは、ドライバーと WSD のサンプル アプリのインストールについてを説明します。
ms.assetid: BF89F0D0-2ED3-4900-996F-BB7B9C8C9B80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36f5f9d432dc584864a1a6efb29c924fcf24382
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527698"
---
# <a name="install-the-driver-and-sample-app"></a>ドライバーとサンプル アプリをインストールします。


このセクションでは、ドライバーと WSD のサンプル アプリのインストールについてを説明します。

## <a name="install-the-driver-on-a-windows81-machine"></a>Windows 8.1 コンピューターでドライバーをインストールします。


SDK の印刷、ドライバーの .inf ファイルを選択すると、3 D に含まれる印刷ドライバーをインストールする、ファイルを右クリックし、**インストール**します。

## <a name="install-the-sample-app"></a>サンプル アプリをインストールします。


まず、Microsoft Visual Studio 2013 (Professional または Ultimate) をインストールして、適用するには、サービス パックや更新プログラムが必要です。

サンプル実装は、WS 印刷プロトコル要求に応答する http ハンドラーを ASP.NET で実装される Microsoft インターネット インフォメーション サービス (IIS) web サービスで構成されます。

有向の検出は、UDP を検出せず、http プロトコルで動作するように web サービスの実行を操作できます。

### <a name="installation-requirements"></a>インストール要件

Windows コンピューターで、web サービスの展開では、IIS と ASP.NET の Microsoft .NET 4.5 と共にインストールされているマシンがあることが必要です。

### <a name="install-iis"></a>IIS のインストール

1.  IIS をインストールするキーを押して、 **Windows** + **R**キーの組み合わせを表示、**実行**ダイアログを入力し、`appwiz.cpl`キーを押します **」と入力**.

    ![実行](images/wsd-app-1.png)

    コントロール パネルが開き**プログラムと機能**します。

2.  **コントロール パネル ホーム**ウィンドウで、をクリックして**オンまたはオフにする Windows 機能**します。

    ![プログラムと機能](images/wsd-app-2.png)

3.  **Windows 機能**ダイアログ ボックスで、**インターネット インフォメーション サービス**チェック ボックスをオンします。

    ![windows の機能](images/wsd-app-3.png)

4.  展開、**インターネット インフォメーション サービス**チェック ボックスをオンし、展開**World Wide Web サービス**します。

    ![world wide web サービス](images/wsd-app-4.png)

5.  展開**アプリケーション開発機能**を選択し、サブ機能を次に示します。

    ![アプリケーション開発機能](images/wsd-app-5.png)

6.  **[OK]** をクリックします。 **変更を適用する**ダイアログに、インストールの進行状況を表示します。

    ![変更を適用します。](images/wsd-app-6.png)

7.  ときに、**変更を適用する**ダイアログ ボックスが閉じ、ブラウザーを開きに移動します http://localhostします。

    ![localhost](images/wsd-app-7.png)

### <a name="publish-the-project"></a>プロジェクトを発行します

Localhost を web サービスをデプロイするハンドラーのプロジェクトを発行します。

![web を発行します。](images/wsd-app-8.png)

発行が成功するを参照する http://localhost送信の空のファイルになります。 ハンドラーがない場合セットアップ正しく、するは、エラー メッセージを受信または可能性のある既定の IIS web ページを参照してください。

切り替えることができます、 **DefaultAppPool**でを実行する、 **NetworkService** id と、それは引き続き期待どおりに動作します。 **DefaultAppPool**も、ネットワーク経由でも作業する必要があります。

### <a name="verify-site-bindings"></a>サイト バインドを確認します。

IPv6 をサポートする必要がある場合は、IPv6 のため、ASP.NET サイトのバインドが作成されたことを確認します。

ハンドラーのプロジェクトにプロジェクトを発行する**既定の Web サイト**します。

既定では、サイトは、すべての IP アドレスでポート 80 にバインドされます。

![サイトのバインド](images/wsd-app-9.png)

### <a name="update-windows-firewall"></a>Windows ファイアウォールを更新します。

既定では、Windows のブロックは、マシンのポート 80 をトラフィックを World Wide Web サービス (http) を許可するための Windows ファイアウォールを更新する必要があります。 これをオンに、せず、クライアントからの受信 http 要求は失敗します。

![windows ファイアウォール](images/wsd-app-10.png)

### <a name="install-the-fabrikam-printer"></a>Fabrikam のプリンターをインストールします。

### <a name="directed-discovery-via-http-endpoint"></a>Http エンドポイント経由で有向の検出

1.  開いている**デバイスとプリンター**で**コントロール パネル**します。

2.  選択**プリンターの追加**します。

3.  選択**は目的のプリンターの一覧に表示されない**します。

    ![プリンターを追加します。](images/wsd-app-11.png)

4.  選択**TCP/IP アドレスまたはホスト名を使用してプリンターを追加する**します。

    ![その他のオプションを使用してプリンターを検索します。](images/wsd-app-12.png)

5.  選択**Web サービスのデバイス**から**デバイスの種類**一覧。

    ![デバイスの種類を選択します。](images/wsd-app-13.png)

6.  ホスト名または IP アドレスを入力し、をクリックして**次**します。

    **問い合わせ中プリンター.** 進行状況バーが表示されます。

    ![ホスト名または ip アドレスを入力します。](images/wsd-app-14.png)

    Fabrikam のプリンターがインストールされている場合、次のメッセージが表示されます。

    ![fabrikam の 3d プリンターがインストールされています。](images/wsd-app-15.png)

### <a name="ad-hoc-discovery-via-udp-multicast"></a>UDP マルチキャストを使用してアドホック探索

ポート 3702 で検出イベントをリッスンする UDP サーバーを実装することによって、アドホック探索を実行できます。

Exchange のシーケンスの詳細については、[検出し、メタデータ交換のメッセージ パターン](https://msdn.microsoft.com/library/windows/desktop/bb513677.aspx)を参照してください。

 

 




