---
Description: Use the USB User-Mode Driver template provided with Microsoft Visual Studio to write a UMDF client driver.
title: 最初、USB クライアント ドライバー (UMDF) を記述する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a636c0ff23adc0c4682a4d8f80475273a6250875
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552872"
---
# <a name="how-to-write-your-first-usb-client-driver-umdf"></a>最初、USB クライアント ドライバー (UMDF) を記述する方法


このトピックでは使用し、 **USB ユーザー モード ドライバー**ユーザー モード ドライバー フレームワーク (UMDF) を記述する、Microsoft Visual Studio 2012 に付属するテンプレートのベースのクライアント ドライバー。 を構築してクライアント ドライバーをインストールしたら、クライアント ドライバーを表示します**デバイス マネージャー**し、デバッガーでドライバーの出力を表示します。

UMDF (このトピックの「フレームワークと呼ばれます) は、コンポーネント オブジェクト モデル (COM) に基づきます。 フレームワークのすべてのオブジェクトを実装する必要があります[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)とそのメソッドでは、 [ **QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521)、 [ **AddRef**](https://msdn.microsoft.com/library/windows/desktop/ms691379)、および[**リリース**](https://msdn.microsoft.com/library/windows/desktop/ms682317)、既定では。 **AddRef**と**リリース**クライアント ドライバーは、参照カウントを維持する必要はありませんので、メソッドがオブジェクトの有効期間を管理します。 **QueryInterface**メソッドは、Windows Driver Frameworks (WDF) オブジェクト モデルの他のフレームワーク オブジェクト インターフェイス ポインターを取得するクライアント ドライバーを使用できます。 Framework オブジェクトでは、ドライバーの複雑なタスクを実行し、Windows との対話します。 Framework の特定のオブジェクトは、フレームワークと対話するためのクライアント ドライバーを有効にするインターフェイスを公開します。

UMDF ベースのクライアント ドライバーは、インプロセス COM サーバー (DLL) として実装し、C++ は USB デバイスのクライアント ドライバーを記述するための優先言語。 通常、クライアント ドライバーは、フレームワークによって公開されているいくつかのインターフェイスを実装します。 このトピックでは、クライアント ドライバーで定義されているコールバック クラスとして framework インターフェイスを実装するクラスを参照します。 これらのクラスをインスタンス化した後、結果のコールバック オブジェクトは特定のフレームワーク オブジェクトと提携しました。 このパートナーシップには、クライアント ドライバーのデバイスや、フレームワークによって報告されるシステムに関連するイベントに応答する機会が与えられます。 Windows では、特定のイベントに関する、フレームワークに通知、たびに、フレームワークがある場合、クライアント ドライバーのコールバックを呼び出します。 それ以外の場合、フレームワークは、イベントの既定の処理を続行します。 テンプレート コードでは、ドライバー、デバイス、およびキュー コールバック lasses を定義します。

テンプレートによって生成されたソース コードに関する詳細については、次を参照してください。 [USB クライアント ドライバーの UMDF テンプレート コードを理解する](understanding-the-umdf-template-code-for-usb.md)します。

### <a name="prerequisites"></a>前提条件

開発、デバッグ、およびユーザー モード ドライバーをインストールする、2 台のコンピューターが必要です。

-   Windows 7 または Windows オペレーティング システムの以降のバージョンを実行しているホスト コンピューター。 ホスト コンピューターは、開発環境の作成し、デバッグには、ドライバーです。
-   たとえば、Windows 8 でのドライバーをテストする対象のコンピュータがオペレーティング システムのバージョンを実行しています。 対象のコンピュータがユーザー モード ドライバーをデバッグして、デバッガーのいずれかです。

場合によって、ホストとターゲット コンピューターが同じバージョンの Windows で実行されている 1 台のコンピューターが Windows 7、Windows のそれ以降のバージョンを実行していることができます。 このトピックでは、開発、デバッグ、および、ユーザー モード ドライバーのインストールの 2 台のコンピューターを使用していることを前提としています。

開始する前に、次の要件を満たしていることを確認します。

**ソフトウェア要件**

-   ホスト コンピューターでは、Visual Studio 2012 にします。
-   ホスト コンピューターでは、Windows 8 の最新 Windows Driver Kit (WDK) を持ちます。

    キットには、ヘッダー、ライブラリ、ツール、ドキュメント、およびデバッグ ツールを開発するために必要なビルド、および USB クライアント ドライバーをデバッグします。 WDK からの最新版を入手できます[、WDK を取得する方法](https://go.microsoft.com/fwlink/p/?linkid=617585)します。

-   ホスト コンピューターでは、Windows 用デバッグ ツールの最新バージョンがあります。 WDK から最新バージョンを取得することもできますを[ダウンロードとデバッグ ツールの Windows にインストール](https://go.microsoft.com/fwlink/p/?linkid=617701)します。
-   2 台のコンピューターを使用している場合は、ユーザー モード デバッグのホストとターゲットのコンピューターを構成する必要があります。 詳細については、次を参照してください。[ユーザー モード デバッグのセットアップでは、Visual Studio](https://msdn.microsoft.com/library/windows/hardware/hh439381)します。

**ハードウェア要件**

クライアント ドライバーを記述する USB デバイスを取得します。 ほとんどの場合、USB デバイスとそのハードウェアの仕様が提供されます。 仕様では、デバイスの機能とサポートされているベンダー コマンドについて説明します。 仕様を使用すると、USB ドライバーとの関連の設計に関する決定の機能を確認できます。

USB ドライバーの開発に慣れていない場合は、OSR USB FX2 ラーニング キットを使用して、WDK に含まれている USB サンプルを調査します。 ラーニング キットを入手することができます[OSR オンライン](https://go.microsoft.com/fwlink/p/?linkid=617553)します。 USB FX2 デバイスと、クライアント ドライバーを実装するすべての必要なハードウェア仕様が含まれています。

**推奨資料**

-   [すべてのドライバー開発者向けの概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)
-   [デバイス ノードとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/ff554721)
-   [Windows ドライバーの概要](https://msdn.microsoft.com/library/windows/hardware/ff554690)
-   [ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff560027)
-   *Windows Driver Foundation でのドライバーの開発*少額 Orwick と Guy Smith によって書き込まれた、します。 詳細については、次を参照してください。 [WDF のドライバーが開発](https://go.microsoft.com/fwlink/p/?linkid=617702)します。

<a name="instructions"></a>手順
------------

### <a href="" id="generate-the-umdf-driver-code-by-using-the-visual-studio-2012-usb-driver-template"></a>手順 1:Visual Studio 2012 の USB ドライバーのテンプレートを使用して UMDF ドライバーのコードを生成します。

<a href="" id="generate"></a> UMDF ドライバー コードの生成方法については、次を参照してください。 [UMDF ドライバーの作成、テンプレートに基づく](https://msdn.microsoft.com/library/windows/hardware/hh439659)します。

**USB に固有のコードを Visual Studio 2012 で、次のオプションを選択します。**

1.  **新しいプロジェクト** ダイアログ ボックスで、左側のウィンドウで検索して選択**USB です。**
2.  中央のペインで選択**USB ユーザー モード ドライバー**します。

次のスクリーン ショットは**新しいプロジェクト**の ダイアログ ボックス、 **USB ユーザー モード ドライバー**テンプレート。

![visual studio の新しいプロジェクトのオプション](images/umdf-tmpl.png)

このトピックでは、プロジェクトの名前がある前提としています。"MyUSBDriver\_UMDF\_"。 次のファイルが含まれています。

| ファイル                      | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Driver.h;Driver.c         | 宣言および実装するコールバック クラスを定義、 [ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス。 クラスは、フレームワークのドライバー オブジェクトによって呼び出されるメソッドを定義します。 このクラスの主な目的では、クライアント ドライバー用にデバイス オブジェクトを作成します。                                                                                                                                                                     |
| Device.h;Device.c         | 宣言および実装するコールバック クラスを定義、 [ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)インターフェイス。 クラスは、フレームワークのデバイス オブジェクトによって呼び出されるメソッドを定義します。 このクラスの主な目的は、プラグ アンド プレイ (PnP) の状態の変更の結果として発生するイベントを処理するためにです。 クラスは、割り当ても、システムが読み込まれている限り、クライアント ドライバーで必要なリソースを初期化します。 |
| IoQueue.h;IoQueue.c       | 宣言および実装するコールバック クラスを定義、 [ **IQueueCallbackDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852)インターフェイス。 クラスは、フレームワークのキュー オブジェクトによって呼び出されるメソッドを定義します。 このクラスでは、フレームワークでキューに置かれた I/O 要求を取得します。                                                                                                                               |
| internal.h                 | USB デバイスと通信するクライアント ドライバーとユーザー アプリケーションによって共有される一般的な宣言を提供します。 トレース関数とマクロも宣言されています。                                                                                                                                                                                                                                                                          |
| Dllsup.cpp                 | ドライバー モジュールのエントリ ポイントの実装が含まれています。                                                                                                                                                                                                                                                                                                                                                                              |
| *&lt;プロジェクト名&gt;*.inf | INF ファイル、ターゲット コンピューターにクライアント ドライバーをインストールするために必要です。                                                                                                                                                                                                                                                                                                                                                               |
| Exports.def                | エントリがエクスポートする DEF ファイルは、ドライバーのモジュールの関数名をポイントします。                                                                                                                                                                                                                                                                                                                                                                    |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>手順 2:デバイスに関する情報を追加する INF ファイルを変更します。

<a href="" id="modify"></a> ドライバーをビルドする前に、ハードウェア ID 文字列では具体的には、デバイスに関する情報を含むテンプレートの INF ファイルを変更する必要があります。

**ハードウェア ID の文字列を指定するには**

1.  Windows デバイスを列挙し、ホスト コンピューターに USB デバイスをアタッチします。
2.  開く**デバイス マネージャー**し、デバイスのプロパティを開きます。
3.  **詳細** タブで **ハードウェア Id** **プロパティ。**

    デバイスのハードウェア ID は、リスト ボックスに表示されます。 右クリックし、ハードウェア ID の文字列をコピーします。

4.  **ソリューション エクスプ ローラー**、展開**ドライバー ファイル**、し、INF を開きます。
5.  次を置換するハードウェア ID の文字列。

    `[Standard.NT$ARCH$]`

    `%DeviceName%=MyDevice_Install, USB\VID_vvvv&PID_pppp`

通知、 **AddReg**ドライバーの情報 (INF) ファイル内のエントリ。

`[CoInstallers_AddReg] ;`

`HKR,,CoInstallers32,0x00010008,"WudfCoinstaller.dll"`

`HKR,,CoInstallers32,0x00010008,"WudfUpdate_01011.dll"`

`HKR,,CoInstallers32,0x00010008,"WdfCoInstaller01011.dll,WdfCoInstaller"`

`HKR,,CoInstallers32,0x00010008,"WinUsbCoinstaller2.dll"`

- WudfCoinstaller.dll (共同インストーラーの構成)
- WUDFUpdate\_*&lt;バージョン&gt;*.dll (共同インストーラーを再頒布可能パッケージ)
- Wdfcoinstaller<em>&lt;バージョン&gt;</em>.dll (kmdf 共同インストーラー)
- Winusbcoinstaller2.dll ((共同インストーラー Winusb.sys の)
- MyUSBDriver\_UMDF\_.dll (クライアント ドライバー モジュール)

INF AddReg ディレクティブが UMDF を共同インストーラー再頒布可能パッケージを参照しているかどうか (WUDFUpdate\_*&lt;バージョン&gt;*.dll)、構成の共同インストーラー (への参照を行う必要がありますいません。WUDFCoInstaller.dll)。 INF で両方の co-installer を参照すると、インストール エラーが発生します。

すべて UMDF ベースの USB クライアント ドライバーには、2 つの Microsoft から提供されたドライバーが必要です。 reflector と WinUSB します。

-   Reflector など、ドライバーが正常に読み込まれた場合に、カーネル モード スタックの一番上のドライバーとしてリフレクターが読み込まれます。 Reflector は、カーネル モード スタックの最上位のドライバーである必要があります。 この要件を満たすためには、テンプレートの INF ファイルをサービス、INF で下位フィルター ドライバーとして WinUSB としてのリフレクターを指定します。

    `[MyDevice_Install.NT.Services]`

    `AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall  ; flag 0x2 sets this as the service for the device`

    `AddService=WinUsb,0x000001f8,WinUsb_ServiceInstall  ; this service is installed because its a filter.`

-   WinUSB — WinUSB がカーネル モードの USB ドライバー スタックへのゲートウェイをクライアント ドライバーのために、インストール パッケージが Winusb.sys の共同インストーラーを含める必要があります。 別のコンポーネントが読み込まれるには、ユーザー モード DLL、クライアント ドライバーのホスト プロセス (Wudfhost.exe) で、WinUsb.dll をという名前です。 Winusb.dll 公開[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)クライアント ドライバーと WinUSB 間の通信プロセスを簡略化します。

### <a href="" id="build-the-usb-client-driver-code"></a>手順 3:USB クライアント ドライバー コードをビルドします。

<a href="" id="build"></a>
**ドライバーをビルドするには**

1.  Visual Studio 2012 では、ドライバーのプロジェクトまたはソリューションを開きます。
2.  ソリューションを右クリックし、**ソリューション エクスプ ローラー**選択**Configuration Manager**します。
3.  **Configuration Manager**を選択、**アクティブ ソリューション構成**(たとえば、 **Windows 8 のデバッグ**または**Windows 8 Release**)、および**アクティブ ソリューション プラットフォーム**(たとえば、Win32) 興味のあるビルドの種類に対応しています。
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

   **Guid**引数は、クライアント ドライバーのトレース プロバイダーの GUID を指定します。 Microsoft Visual Studio Professional 2012 のプロジェクトで、Trace.h から GUID を取得できます。 別のオプションとしては、次のコマンドを入力し、.guid ファイルで、GUID を指定します。 ファイルには、ハイフンの形式で GUID が含まれています。

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

 

### <a href="" id="view-the-driver-in-device-manager"></a>手順 7:デバイス マネージャーで、ドライバーを表示します。

<a href="" id="devicemanager"></a>
1.  開くには、次のコマンドを入力します。**デバイス マネージャー**します。

    **devmgmt**

2.  いることを確認**デバイス マネージャー**次のノードを示しています。

    **USB デバイス**

    **MyUSBDriver\_UMDF\_デバイス**

### <a href="" id="view-the-output-in-the-debugger"></a>手順 8:デバッガーで、出力を表示します。

トレース メッセージが表示されることを確認、**デバッガーのイミディ エイト ウィンドウ**ホスト コンピューター。

出力は、次のようになります。

``` syntax
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Entry
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Exit
```

<a name="remarks"></a>注釈
-------

フレームワークと、クライアント ドライバーがどのように連携して Windows を操作し、USB デバイスに送信された要求の処理を見てをみましょう。 この図で、システムを UMDF に読み込まれたモジュール-ベースの USB クライアント ドライバー。

![ユーザー モードのクライアント ドライバーのアーキテクチャ](images/umdfstack.png)

各モジュールの目的を次に示します。

-   アプリケーション-USB デバイスと通信する I/O を発行するユーザー モード プロセスを要求します。
-   I/O マネージャー、Windows コンポーネントを I/O 要求パケット (Irp) を表す受信したアプリケーションの要求を作成し、対象デバイスのカーネル モード デバイスのスタックの一番上に転送します。
-   Reflector-カーネル モード デバイス スタック (WUDFRd.sys) の上部にあるインストールされている Microsoft 提供のカーネル モード ドライバー。 Reflector は、クライアント ドライバーのホスト プロセスが I/O マネージャーから受信した Irp をリダイレクトします。 要求を受信したら、フレームワークと、クライアント ドライバーは、要求を処理します。
-   ホスト プロセス、ユーザー モード ドライバー (Wudfhost.exe) を実行するプロセス。 また、フレームワークと I/O ディスパッチャーをホストします。
-   クライアント ドライバー-USB デバイスのユーザー モード関数ドライバー。
-   UMDF: クライアント ドライバーの代わりに Windows とのほとんど対話を処理するフレームワーク モジュール。 クライアント ドライバーがドライバーの一般的なタスクを実行するユーザー モード デバイス ドライバー インターフェイス (Ddi) を公開します。
-   ディスパッチャー、ホスト プロセスで実行されているメカニズムユーザー モード ドライバーによって処理されたおよびユーザー モードのスタックの一番下に達した後に、カーネル モードへの要求を転送する方法を決定します。 図では、ディスパッチャーは、ユーザー モード DLL Winusb.dll に要求を転送します。
-   Winusb.dll—a を公開する Microsoft 提供のユーザー モード DLL [WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)クライアント ドライバーと WinUSB (Winusb.sys、カーネル モードで読み込まれます) の間の通信プロセスを簡略化します。
-   Winusb.sys—a Microsoft 提供のドライバーの USB デバイスのすべての UMDF クライアント ドライバーで必要とされます。 カーネル モードでの USB ドライバー スタックへのゲートウェイとしては、reflector と機能の下、ドライバーをインストールする必要があります。 詳細については、次を参照してください。 [WinUSB](winusb.md)します。
-   USB ドライバー スタックなど、一連のドライバー、Microsoft が提供されている USB デバイスとプロトコル レベルの通信を処理します。 詳細については、次を参照してください。 [Windows での USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)します。

アプリケーションでは、USB ドライバー スタックの要求を行う、たびに、Windows I/O マネージャーは、reflector は、ユーザー モードでのクライアント ドライバーにリダイレクトする、要求を送信します。 クライアント ドライバーでは、要求を処理、内部的に呼び出す特定の UMDF メソッドを呼び出して、 [WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb) WinUSB に要求を送信します。 要求を受信したら WinUSB は要求を処理するか、または USB ドライバー スタックに転送。

## <a name="related-topics"></a>関連トピック
[USB クライアント ドライバーの UMDF テンプレート コードを理解します。](understanding-the-umdf-template-code-for-usb.md)  
[USB のセレクティブがサスペンドを有効にする方法と、USB デバイスの UMDF ドライバーにシステムがスリープ解除](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB クライアント ドライバー開発を入門](getting-started-with-usb-client-driver-development.md)  



