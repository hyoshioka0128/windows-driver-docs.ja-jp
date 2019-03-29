---
Description: In this topic you'll use the USB Kernel-Mode Driver template provided with Microsoft Visual Studio Professional 2012 to write a simple kernel-mode driver framework (KMDF)-based client driver.
title: 初めての USB クライアント ドライバーの記述方法 (KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f0dc7337526e0736a6b9adb850e86e386a0a8ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571966"
---
# <a name="how-to-write-your-first-usb-client-driver-kmdf"></a>初めての USB クライアント ドライバーの記述方法 (KMDF)


このトピックでは使用し、 **USB カーネル モード ドライバー** Microsoft Visual Studio の Professional 2012 書き込む単純なカーネル モード ドライバー フレームワーク (KMDF) に付属するテンプレートのベースのクライアント ドライバー。 を構築してクライアント ドライバーをインストールしたら、クライアント ドライバーを表示します**デバイス マネージャー**し、デバッガーでドライバーの出力を表示します。

テンプレートによって生成されたソース コードに関する詳細については、次を参照してください。 [USB クライアント ドライバーの KMDF テンプレート コードを理解する](understanding-the-kmdf-template-code-for-usb.md)します。

### <a name="prerequisites"></a>前提条件

開発、デバッグ、およびカーネル モード ドライバーをインストールする、2 台のコンピューターが必要です。

-   Windows 7 または Windows オペレーティング システムの以降のバージョンを実行しているホスト コンピューター。 ホスト コンピューターは、開発環境の作成し、デバッグには、ドライバーです。
-   Windows Vista または Windows の以降のバージョンを実行しているターゲット コンピューター。 対象のコンピュータが、カーネル モード ドライバーをデバッグします。

開始する前に、次の要件を満たしていることを確認します。

**ソフトウェア要件**

-   ホスト コンピューターでは、開発環境をホストし、Visual Studio Professional 2012 を持ちます。
-   ホスト コンピューターでは、Windows 8 の最新 Windows Driver Kit (WDK) を持ちます。 キットは、ヘッダー、ライブラリ、ツール、ドキュメントについては、デバッグ ツールを開発するために必要なビルド、デバッグと KMDF ドライバー。 WDK の最新バージョンを取得するには、次を参照してください。 [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)します。
-   ホスト コンピューターでは、Windows 用デバッグ ツールの最新バージョンがあります。 WDK から最新バージョンを取得することもできますを[ダウンロードとデバッグ ツールの Windows にインストール](https://msdn.microsoft.com/windows/hardware/gg463009.aspx)します。
-   Windows Vista または Windows の以降のバージョン、ターゲット コンピューターが実行されています。
-   カーネルのデバッグと、ホストとターゲット コンピューターが構成されます。 詳細については、次を参照してください。[設定、ネットワーク接続のセットアップでは、Visual Studio](https://msdn.microsoft.com/library/windows/hardware/hh439353)します。

**ハードウェア要件**

クライアント ドライバーを記述する USB デバイスを取得します。 ほとんどの場合、USB デバイスとそのハードウェアの仕様が提供されます。 仕様では、デバイスの機能とサポートされているベンダー コマンドについて説明します。 仕様を使用すると、USB ドライバーとの関連の設計に関する決定の機能を確認できます。

USB ドライバーの開発に慣れていない場合は、OSR USB FX2 ラーニング キットを使用して、WDK に含まれている USB サンプルを調査します。 ラーニング キットを入手することができます[OSR オンライン](http://www.osronline.com/)します。 USB FX2 デバイスと、クライアント ドライバーを実装するすべての必要なハードウェア仕様が含まれています。

Microsoft USB Test Tool (MUTT) デバイスを取得することもできます。 MUTT ハードウェアを購入できる[JJG テクノロジ](http://jjgtechnologies.com/mutt.md)します。 デバイスのファームウェアがインストールされているインストールではありません。 ファームウェアをインストールするから MUTT ソフトウェア パッケージをダウンロード[この Web サイト](https://msdn.microsoft.com/windows/hardware/jj590752)MUTTUtil.exe を実行します。 詳細については、パッケージに付属のマニュアルを参照してください。

**推奨資料**

-   [すべてのドライバー開発者向けの概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)
-   [デバイス ノードとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/ff554721)
-   [Windows ドライバーの概要](https://msdn.microsoft.com/library/windows/hardware/ff554690)
-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   *Windows Driver Foundation でのドライバーの開発*少額 Orwick と Guy Smith によって書き込まれた、します。 詳細については、次を参照してください。 [WDF のドライバーが開発](https://msdn.microsoft.com/windows/hardware/gg463318)します。

<a name="instructions"></a>手順
------------

### <a href="" id="generate-the-kmdf-driver-code-by-using-the--visual-studio-professional-2012---usb-driver-template"></a>手順 1:Visual Studio Professional 2012 の USB ドライバーのテンプレートを使用して、KMDF ドライバー コードを生成します。

KMDF ドライバー コードの生成方法については、手順を参照してください。 [KMDF ドライバーの作成、テンプレートに基づく](https://msdn.microsoft.com/library/windows/hardware/hh439654)します。

**USB に固有のコードを Visual Studio Professional 2012 で、次のオプションを選択します。**

1.  **新しいプロジェクト**ダイアログ ボックスで、左側のウィンドウで、 **USB です。**
2.  中央のペインで選択**USB カーネル モード ドライバー**します。

次のスクリーン ショットは**新しいプロジェクト**の ダイアログ ボックス、 **USB カーネル モード ドライバー**テンプレート。

![visual studio の新しいプロジェクトのオプション](images/kmdf-tmpl.png)

このトピックでは、Visual Studio プロジェクトの名前がある前提としています。"MyUSBDriver\_"。 次のファイルが含まれています。

| ファイル                      | 説明                                                                                                          |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| Public.h                   | USB デバイスと通信するクライアント ドライバーとユーザー アプリケーションによって共有される一般的な宣言を提供します。 |
| *&lt;プロジェクト名&gt;*.inf | ターゲット コンピューター上のクライアント ドライバーのインストールに必要な情報が含まれています。                                   |
| Trace.h                    | トレース関数とマクロを宣言します。                                                                               |
| Driver.h;Driver.c         | 宣言し、ドライバーのエントリ ポイントとイベントのコールバック ルーチンを定義します。                                                |
| Device.h;Device.c         | 宣言し、準備-ハードウェア イベントのイベント コールバック ルーチンを定義します。                                          |
| Queue.h;Queue.c           | 宣言し、フレームワークのキュー オブジェクトによって発生するイベントのイベント コールバック ルーチンを定義します。                 |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>手順 2:デバイスに関する情報を追加する INF ファイルを変更します。

ドライバーをビルドする前に、ハードウェア ID 文字列では具体的には、デバイスに関する情報を含むテンプレートの INF ファイルを変更する必要があります。

**ソリューション エクスプ ローラー****ドライバー ファイル**、INF ファイルをダブルクリックします。

INF ファイルでは、製造元とプロバイダーの名前をデバイス セットアップ クラスなどの情報を提供し、具合です。 提供する必要がある情報の 1 つは、デバイスのハードウェア識別子です。

ハードウェア ID の文字列を提供します。

1.  Windows デバイスを列挙し、ホスト コンピューターに USB デバイスをアタッチします。
2.  開く**デバイス マネージャー**し、デバイスのプロパティを開きます。
3.  **詳細** タブで **ハードウェア Id** **プロパティ。**

    デバイスのハードウェア ID は、リスト ボックスに表示されます。 右クリックし、ハードウェア ID の文字列をコピーします。

4.  USB を置き換える\\VID\_vvvv & PID\_pppp、ハードウェア ID の文字列では、次の行にします。

    `[Standard.NT$ARCH$] %MyUSBDriver_.DeviceDesc%=MyUSBDriver__Device, USB\VID_vvvv&PID_pppp`

### <a href="" id="build-the-usb-client-driver-code"></a>手順 3:USB クライアント ドライバー コードをビルドします。

**ドライバーをビルドするには**

1.  Visual Studio Professional 2012 で、ドライバーのプロジェクトまたはソリューションを開く
2.  ソリューションを右クリックし、**ソリューション エクスプ ローラー**選択**Configuration Manager**します。
3.  **Configuration Manager**を選択、**アクティブ ソリューション構成**(たとえば、 **Windows 8 のデバッグ**または**Windows 8 Release**) および**アクティブ ソリューション プラットフォーム**(たとえば、Win32) に関心があるビルドの種類に対応しています。
4.  **ビルド** メニューのをクリックして**ソリューションのビルド**します。

詳細については、次を参照してください。[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)します。

### <a href="" id="configure-a-computer-for-testing-and-debugging"></a>手順 4:テストとデバッグ用のコンピューターを構成します。

でテストおよびドライバーをデバッグするには、ホスト コンピューターとターゲット コンピューターのドライバーにデバッガーを実行します。 ここまでは、ドライバーをビルドするのにホスト コンピューターで Visual Studio を使用しています。 次に、ターゲット コンピューターを構成する必要があります。 対象のコンピュータを構成する手順については、[ドライバーの展開とテスト用にプロビジョニング](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。

### <a href="" id="enable-tracing-for-kernel-debugging"></a>手順 5:カーネルのデバッグ トレースを有効にします。

テンプレート コードには、関数呼び出しを追跡するのに役立ついくつかのトレース メッセージ (TraceEvents) が含まれています。 ソース コード内のすべての関数とルーチンの終了をマークするトレース メッセージを格納します。 エラーについては、トレース メッセージには、エラー コードと意味のある文字列が含まれています。 ドライバーのプロジェクトで WPP トレースを有効にするため、ビルド プロセス中に作成された PDB シンボル ファイルには、トレース メッセージ書式命令にはが含まれています。 WPP トレース用のホストとターゲットのコンピューターを構成するには、ドライバーは、ファイルやデバッガーにトレース メッセージを送信できます。

**ホスト コンピューター WPP トレースを構成するには**

1. 手順については、PDB シンボル ファイルの書式設定のトレース メッセージを抽出することで、トレース メッセージの形式 (TMF) ファイルを作成します。

   Tracepdb.exe を使用して、TMF ファイルを作成することができます。 ツールがである、 <em>&lt;インストール フォルダー&gt;</em>Windows キット\\8.0\\bin\\*&lt;アーキテクチャ&gt;* WDK のフォルダー。 次のコマンドは、ドライバーのプロジェクトの TMF ファイルを作成します。

   **tracepdb -f \[PDBFiles\] -p \[TMFDirectory\]**

   **-F**オプションは、場所と PDB シンボル ファイルの名前を指定します。 **-P** Tracepdb によって作成される TMF ファイルの場所を指定します。 詳細については、次を参照してください。 [ **Tracepdb コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff553043)します。

   指定した位置には、3 つのファイル (.c ファイルで、プロジェクトごとに 1 つ) を確認します。 GUID ファイル名が表示されます。

2. デバッガーでは、次のコマンドを入力します。
   1.  **.load Wmitrace**

       Wmitrace.dll 拡張機能を読み込みます。

   2.  **.chain**

       デバッガー拡張が読み込まれていることを確認します。

   3.  **!wmitrace.searchpath +***&lt;TMF file location&gt;*

       デバッガーの拡張機能の検索パスに TMF ファイルの場所を追加します。

       次のように出力します。

       `Trace Format search path is: 'C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE;c:\drivers\tmf'`

**WPP トレースの対象のコンピューターを構成するには**

1. ターゲット コンピューターにトレース ログ ツールがあることを確認します。 ツールがである、 <em>&lt;インストール\_フォルダー&gt;</em>Windows キット\\8.0\\ツール\\*&lt;arch&gt;*  WDK のフォルダー。 詳細については、次を参照してください。 [ **Tracelog コマンド構文**](https://msdn.microsoft.com/library/windows/hardware/ff553012)します。
2. 開く、**コマンド ウィンドウ**管理者として実行します。
3. 次のコマンドを入力します。

   **tracelog -start MyTrace -guid \#c918ee71-68c7-4140-8f7d-c907abbcb05d -flag 0xFFFF -level 7-rt -kd**

   コマンドは、MyTrace をという名前のトレース セッションを開始します。

   **Guid**引数は、クライアント ドライバーのトレース プロバイダーの GUID を指定します。 Visual Studio Professional 2012 のプロジェクトで、Trace.h から GUID を取得できます。 別のオプションとしては、次のコマンドを入力し、.guid ファイルで、GUID を指定します。 ファイルには、ハイフンの形式で GUID が含まれています。

   **トレース ログ-開始 MyTrace - guid の c:\\ドライバー\\Provider.guid-0 xffff をフラグ-7 rt kd をレベル**

   トレース セッションを停止するには、次のコマンドを入力します。

   **tracelog -stop MyTrace**

### <a href="" id="deploy-the-driver-on-the-target-computer"></a>手順 6:ターゲット コンピューター上のドライバーを展開します。

1. **ソリューション エクスプ ローラー**ウィンドウで、右クリックして、 <em>&lt;プロジェクト名&gt;</em>**パッケージ**、選択**プロパティ**.
2. 左側のウィンドウに移動します**構成プロパティ&gt;ドライバー インストール&gt;展開**します。
3. 有効化の展開をドライバー ストアにインポートを確認します。
4. **リモート コンピューター名**、ターゲット コンピューターの名前を指定します。
5. **[Install and Verify (インストールと確認)]** を選びます。
6. **[OK]** をクリックします。
7. **[デバッグ]** メニューの **[デバッグ開始]** をクリックするか、キーボードで **F5** キーを押します。

**注**  は*いない*下で、デバイスのハードウェア ID を指定**ハードウェア ID のドライバーの更新プログラム**。 ドライバーの情報 (INF) ファイルにのみ、ハードウェア ID を指定する必要があります。

 

Visual Studio Professional 2012 で、ターゲット システムにドライバーを展開する方法の詳細については、次を参照してください。[テスト コンピューターにドライバーを展開する](https://msdn.microsoft.com/windows-drivers/develop/deploying_a_driver_to_a_test_computer)します。

デバイス マネージャーを使用して、ターゲット コンピューターでドライバーを手動でインストールできます。 コマンド プロンプトからドライバーをインストールする場合は、これらのユーティリティを使用できます。

-   [PnPUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419)

    このツールは、Windows 付属します。 Windows では\\System32 します。 このユーティリティを使用して、ドライバーをドライバー ストアに追加することができます。

    ``` syntax
    C:\>pnputil /a m:\MyDriver_.inf
    Microsoft PnP Utility

    Processing inf : MyDriver_.inf
    Driver package added successfully.
    Published name : oem22.inf
    ```

    詳細については、次を参照してください。 [PnPUtil 例](https://msdn.microsoft.com/library/windows/hardware/ff550428)します。

-   [**DevCon Update**](https://msdn.microsoft.com/library/windows/hardware/ff544832)

    このツールには、WDK します。 インストールし、ドライバーの更新に使用できます。

    ``` syntax
    devcon update c:\windows\inf\MyDriver_.inf USB\VID_0547&PID_1002\5&34B08D76&0&6
    ```

### <a href="" id="view-the-driver-in-device-manager"></a>手順 7:デバイス マネージャーで、ドライバーを表示します。

1.  開くには、次のコマンドを入力します**デバイス マネージャー**:。

    **devmgmt**

2.  いることを確認**デバイス マネージャー**次のノードのノードを示しています。

    **サンプル**

    **MyUSBDriver\_デバイス**

### <a href="" id="view-the-output-in-the-debugger"></a>手順 8:デバッガーで、出力を表示します。

Visual Studio は、最初の進行状況を表示、**出力**ウィンドウ。 それが開き、**デバッガーのイミディ エイト ウィンドウ**します。 トレース メッセージが、デバッガー ホスト コンピューター上に表示されることを確認します。 、このような出力になります、"MyUSBDriver\_"ドライバー モジュールの名前を指定します。

```cpp
[3]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverContextCleanup Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Exit
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Entry
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Exit
```

## <a name="related-topics"></a>関連トピック
[USB クライアント ドライバーの KMDF テンプレート コードを理解します。](understanding-the-kmdf-template-code-for-usb.md)  
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  



