---
title: ユニバーサル Hello World ドライバー (KMDF) の作成
description: このトピックでは、カーネルモード ドライバー フレームワーク (KMDF) を使ってユニバーサル Windows ドライバーを作成する方法について説明します。 Microsoft Visual Studio テンプレートを使って開始し、別のコンピューターにドライバーを展開してインストールします。
ms.assetid: B4200732-67B5-4BD9-8852-81387912A9A4
keywords:
- KMDF Hello World
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2d43b1c8593473a5724208048d9acfa78803fe95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825163"
---
# <a name="write-a-universal-hello-world-driver-kmdf"></a>ユニバーサル Hello World ドライバー (KMDF) の作成


このトピックでは、カーネルモード ドライバー フレームワーク (KMDF) を使って非常に小さい[ユニバーサル Windows ドライバー](https://docs.microsoft.com/windows-hardware/drivers)を作成し、ドライバーをインストールして個別のコンピューターに展開する方法について説明します。 

最初に、[Microsoft Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=698539)、[Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)、および [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?LinkId=733614) がインストールされていることを確認します。

[Debugging Tools for Windows](https://go.microsoft.com/fwlink/p?linkid=223405) は、WDK のインストールに含まれています。

## <a name="create-and-build-a-driver"></a>ドライバーの作成とビルド


1.  Microsoft Visual Studio を開きます。 **[ファイル]** メニューの **[新規] &gt; [プロジェクト]** をクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[Visual C++] &gt; [Windows ドライバー] &gt; [WDF]** の順に移動します。
3.  中央のウィンドウで、 **[Kernel Mode Driver, Empty (KMDF) (カーネル モード ドライバー, 空 (KMDF))]** を選びます。
4.  **[名前]** フィールドに、プロジェクト名として「KmdfHelloWorld」と入力します。

    > [!NOTE]
    > 新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
     

5.  **[場所]** フィールドに、新規プロジェクトを作るディレクトリを入力します。
6.  **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。 **[OK]** をクリックします。

    ![[新しいプロジェクト] ダイアログ ボックスのスクリーン ショット](images/vs2015-new-project-kmdf-empty.png)

    Visual Studio により、1 つのプロジェクトと 1 つのソリューションが作られます。 これらは、次に示すように、 **[ソリューション エクスプローラー]** ウィンドウに表示されます ([ソリューション エクスプローラー] ウィンドウが表示されない場合は、 **[表示]** メニューの **[ソリューション エクスプローラー]** を選びます)。ソリューションには、KmdfHelloWorld という名前のドライバー プロジェクトがあります。

    ![[ソリューション エクスプローラー] ウィンドウのスクリーン ショットと、ソリューションと空のドライバー プロジェクト (kmdfhelloworld) を表示した状態](images/vs2015-kmdf-hello-world-solution-explorer.png)

7.  **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfHelloWorld]** プロジェクトを右クリックして、 **[プロパティ]** を選びます。 **[構成プロパティ] &gt; [Driver Settings (ドライバーの設定)] &gt; [全般]** の順に移動し、 **[ターゲット プラットフォーム]** が既定で **[ユニバーサル]** に設定されていることを確認します。  **[キャンセル]** をクリックします。

8.  **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfHelloWorld]** プロジェクトを再度右クリックして、 **[追加] &gt; [新しい項目]** を選びます。
9.  **[新しい項目の追加]** ダイアログ ボックスで、 **[C++ ファイル]** を選びます。 **[名前]** に「Driver.c」と入力します。

    > [!NOTE]
    > ファイル名拡張子は、 **.cpp** ではなく **.c** です。

     **[追加]** をクリックします。 次に示すように、Driver.c ファイルが [ソース ファイル] の下に追加されます。

    ![[ソリューション エクスプローラー] ウィンドウのスクリーン ショット (ドライバー プロジェクトに Driver.c ファイルが追加された状態)](images/firstdriverkmdfsmall03.png)

## <a name="write-your-first-driver-code"></a>初めてのドライバー コードの作成

空の Hello World プロジェクトを作成し、Driver.c ソース ファイルを追加したので、ドライバーが 2 つの基本的なイベントのコールバック関数を実装して実行するために必要な最も基本的なコードを記述します。 

1. Driver.c では、これらのヘッダーを含めることで起動します。

    ```C++
    #include <ntddk.h>
    #include <wdf.h>
    ```

    [Ntddk.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk) には、すべてのドライバーのコア Windows カーネルの定義が含まれ、[Wdf.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf) には、Windows Driver Framework (WDF) に基づくドライバーの定義が含まれます。 

2. 次に、使用する 2 つのコールバックの宣言を指定します。

    ```C++
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD KmdfHelloWorldEvtDeviceAdd;
    ```

3. 次のコードを使用して *DriverEntry* を記述します。

    ```C++
    NTSTATUS 
    DriverEntry(
        _In_ PDRIVER_OBJECT     DriverObject, 
        _In_ PUNICODE_STRING    RegistryPath
    )
    {
        // NTSTATUS variable to record success or failure
        NTSTATUS status = STATUS_SUCCESS;
        
        // Allocate the driver configuration object
        WDF_DRIVER_CONFIG config;
        
        // Print "Hello World" for DriverEntry
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: DriverEntry\n" ));

        // Initialize the driver configuration object to register the
        // entry point for the EvtDeviceAdd callback, KmdfHelloWorldEvtDeviceAdd
        WDF_DRIVER_CONFIG_INIT(&config, 
                               KmdfHelloWorldEvtDeviceAdd
                               );

        // Finally, create the driver object
        status = WdfDriverCreate(DriverObject, 
                                 RegistryPath, 
                                 WDF_NO_OBJECT_ATTRIBUTES, 
                                 &config, 
                                 WDF_NO_HANDLE
                                 );
        return status;
    }
    ```

    [*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) はすべてのドライバーのエントリ ポイントで、多くのユーザー モード アプリケーションに使用される `Main()` と同様です。 *DriverEntry* には、ドライバー全体の構造とリソースを初期化する役割があります。 この例では、 *DriverEntry* の "Hello World" を出力し、*EvtDeviceAdd* コールバックのエントリ ポイントを登録するためのドライバー オブジェクトを構成し、ドライバー オブジェクトを作成して返しました。 

    ドライバー オブジェクトは、ドライバーで作成する可能性のあるその他すべてのフレームワーク オブジェクトの親オブジェクトとして機能し、デバイス オブジェクト、I/O キュー、タイマー、スピンロックなどを含みます。 フレームワーク オブジェクトの詳細については、「[フレームワーク オブジェクトの紹介](../wdf/introduction-to-framework-objects.md)」を参照してください。

    > [!TIP]
    > *DriverEntry* には、コード分析とデバッグに役立てるために "DriverEntry" という名前を維持することを強くお勧めします。

4. 次に、次のコードを使用して、*KmdfHelloWorldEvtDeviceAdd* を記述します。

    ```C++
    NTSTATUS 
    KmdfHelloWorldEvtDeviceAdd(
        _In_    WDFDRIVER       Driver, 
        _Inout_ PWDFDEVICE_INIT DeviceInit
    )
    {
        // We're not using the driver object,
        // so we need to mark it as unreferenced
        UNREFERENCED_PARAMETER(Driver);

        NTSTATUS status;

        // Allocate the device object
        WDFDEVICE hDevice;    

        // Print "Hello World"
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: KmdfHelloWorldEvtDeviceAdd\n" ));
        
        // Create the device object
        status = WdfDeviceCreate(&DeviceInit, 
                                 WDF_NO_OBJECT_ATTRIBUTES,
                                 &hDevice
                                 );
        return status;
    }
    ```

    [*EvtDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) は、デバイスが到着したことが検出されたときに、システムによって呼び出されます。 その役割は、デバイスの構造体とリソースを初期化することです。 この例では、単に *EvtDeviceAdd* の "Hello World" のメッセージを出力し、デバイス オブジェクトを作成して返しました。 記述するその他のドライバーでは、ハードウェアの I/O キューを作成したり、デバイス固有の情報のための*デバイス コンテキスト*記憶域スペースを設定したり、デバイスを準備するために必要なその他のタスクを実行したりする場合があります。

    > [!TIP]
    > デバイスの追加コールバックでは、ドライバーの名前をプレフィックスとして名前を付けた方法に注目してください (*KmdfHelloWorld*EvtDeviceAdd)。 一般に、他のドライバーの関数と区別できるようにするために、この方法で、ドライバーの関数の名前を付けることをお勧めします。 *DriverEntry* だけはまさにその名前を付ける必要があります。

5. 完全な Driver.c は、次のようになります。

    ```C++
    #include <ntddk.h>
    #include <wdf.h>
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD KmdfHelloWorldEvtDeviceAdd;

    NTSTATUS 
    DriverEntry(
        _In_ PDRIVER_OBJECT     DriverObject, 
        _In_ PUNICODE_STRING    RegistryPath
    )
    {
        // NTSTATUS variable to record success or failure
        NTSTATUS status = STATUS_SUCCESS;
        
        // Allocate the driver configuration object
        WDF_DRIVER_CONFIG config;
        
        // Print "Hello World" for DriverEntry
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: DriverEntry\n" ));

        // Initialize the driver configuration object to register the
        // entry point for the EvtDeviceAdd callback, KmdfHelloWorldEvtDeviceAdd
        WDF_DRIVER_CONFIG_INIT(&config, 
                               KmdfHelloWorldEvtDeviceAdd
                               );

        // Finally, create the driver object
        status = WdfDriverCreate(DriverObject, 
                                 RegistryPath, 
                                 WDF_NO_OBJECT_ATTRIBUTES, 
                                 &config, 
                                 WDF_NO_HANDLE
                                 );
        return status;
    }

    NTSTATUS 
    KmdfHelloWorldEvtDeviceAdd(
        _In_    WDFDRIVER       Driver, 
        _Inout_ PWDFDEVICE_INIT DeviceInit
    )
    {
        // We're not using the driver object,
        // so we need to mark it as unreferenced
        UNREFERENCED_PARAMETER(Driver);

        NTSTATUS status;

        // Allocate the device object
        WDFDEVICE hDevice;    

        // Print "Hello World"
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: KmdfHelloWorldEvtDeviceAdd\n" ));
        
        // Create the device object
        status = WdfDeviceCreate(&DeviceInit, 
                                 WDF_NO_OBJECT_ATTRIBUTES,
                                 &hDevice
                                 );
        return status;
    }
    ```

6. Driver.c を保存します。

この例は、ドライバーの基本概念を示します。ドライバーは初期化されると、何かが必要なときにシステムがドライバーを呼び出すのを待機する "コールバックのコレクション" です。 これには、新しいデバイス到着イベント、ユーザー モード アプリケーションからの I/O 要求、システムの電源のシャットダウン イベント、別のドライバーからの要求、ユーザーが突然デバイスを取り外したときの突然の削除イベントなどがあります。 さいわい、"Hello World" と言うために、ドライバーとデバイスの作成についてのみ心配するだけで済みました。

次に、ドライバーをビルドします。

## <a name="build-the-driver"></a>ドライバーのビルド

1. **[ソリューション エクスプローラー]** ウィンドウで、 **[ソリューション 'KmdfHelloWorld' (1 プロジェクト)]** を右クリックして **[構成マネージャー]** をクリックします。 ドライバー プロジェクトに対する構成とプラットフォームを選びます。 この作業では、**Debug** と **x64** を選びます。

2. **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfHelloWorld]** を右クリックして、 **[プロパティ]** を選びます。 **[Wpp Tracing (Wpp トレース)] &gt; [すべてのオプション]** で、 **[Run Wpp tracing (Wpp トレースの実行)]** を **[いいえ]** に設定します。 **[適用]** をクリックし、 **[OK]** をクリックします。
3. ドライバーをビルドするには、 **[ビルド]** メニューの **[ソリューションのビルド]** を選びます。 Visual Studio の **[出力]** ウィンドウにビルドの進行状況が表示されます ( **[出力]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[出力]** をクリックします)。ソリューションのビルドが成功したことを確認したら、Visual Studio を閉じることができます。
4. ビルドされたドライバーを確認するには、エクスプローラーで **[KmdfHelloWorld]** フォルダーに移動し、**C:\\KmdfHelloWorld\\x64\\Debug\KmdfHelloWorld** に移動します。 フォルダーには以下が含まれています。

    -   KmdfHelloWorld.sys -- カーネル モード ドライバー ファイル
    -   KmdfHelloWorld.inf -- ドライバーをインストールするときに Windows で使われる情報ファイル
    -   KmdfHelloWorld.cat -- ドライバーのテスト署名を検証するときにインストーラーで使われるカタログ ファイル


> [!TIP]
> ドライバーのビルド時に `DriverVer set to a date in the future` が表示された場合、ドライバー プロジェクトの設定を Inf2Cat が `/uselocaltime` を設定するように変更します。 このためには、 **[構成プロパティ] -> [Inf2Cat] -> [全般] -> [Use Local Time]\(現地時刻の使用\)** を使用します。 これで、[Stampinf](../devtest/stampinf-command-options.md) と Inf2Cat の両方で現地時刻が使用されます。

## <a name="span-iddeploy_the_driverspanspan-iddeploy_the_driverspanspan-iddeploy_the_driverspandeploy-the-driver"></a><span id="Deploy_the_driver"></span><span id="deploy_the_driver"></span><span id="DEPLOY_THE_DRIVER"></span>ドライバーの展開

通常、ドライバーのテストと展開には、デバッガーとドライバーがそれぞれ別のコンピューター上で実行されます。 デバッガーを実行するコンピューターを*ホスト コンピューター*、ドライバーを実行するコンピューターを*ターゲット コンピューター*と呼びます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。

ここまでは、ホスト コンピューター上の Visual Studio を使ってドライバーのビルドを行いました。 次にターゲット コンピューターの構成が必要です。 

1. 「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](provision-a-target-computer-wdk-8-1.md)」の手順に従ってください。

    > [!TIP]
    > 手順に従って、ネットワーク ケーブルを使用して自動的に対象のコンピューターをプロビジョニングする場合は、ポートとキーを書き留めます。 デバッグの手順の後半でそれを使用します。 この例では、ポートに **50000**、キーに **1.2.3.4** を使用します。
    >
    > 実際のドライバー デバッグのシナリオでは、KDNET で生成されたキーを使用することをお勧めします。 KDNET を使用してランダム キーを生成する方法の詳細については、[ドライバーのデバッグ - ステップ バイ ステップ ラボ (Sysvad カーネル モード)](../debugger/debug-universal-drivers--kernel-mode-.md)のトピックを参照してください。

2.  ホスト コンピューター上で、Visual Studio でソリューションを開きます。 KmdfHelloWorld フォルダーにあるソリューション ファイル (KmdfHelloWorld.sln) をダブルクリックしてソリューションを開くこともできます。
3.  **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfHelloWorld]** プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
4.  次に示すように、 **[KmdfHelloWorld のプロパティ ページ]** ウィンドウで、 **[構成プロパティ] &gt; [Driver Install (ドライバーのインストール)] &gt; [配置]** の順に移動します。
5.  **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
6.  **[Target Device Name (ターゲット デバイス名)]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。 この作業では、MyTestComputer というコンピューターを使います。
7.  **[Hardware ID Driver Update (ハードウェア ID のドライバーの更新)]** をクリックして、ドライバーのハードウェア ID を入力します。 この例では、ハードウェア ID は Root\\KmdfHelloWorld です。 **[OK]** をクリックします。

    ![[kmdfhelloworld プロパティ ページ] ウィンドウのスクリーン ショット ([ドライバーのインストール] と [展開] が選ばれた状態) ](images/vs2015-kmdf-hello-world-property-pages.png)

    >[!NOTE]
    > この作業のハードウェア ID は特定のハードウェアを識別するものではありません。 [デバイス ツリー](device-nodes-and-device-stacks.md)上でルート ノードの子として設定される架空のデバイスを表します。 実際のハードウェアについては、 **[Hardware ID Driver Update] (ハードウェア ID のドライバーの更新)** ではなく、 **[Install and Verify] (インストールと確認)** をクリックします。 ハードウェア ID は、ドライバーの情報ファイル (INF) に記載されています。 **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfHelloWorld] &gt; [Driver Files (ドライバー ファイル)]** に移動し、KmdfHelloWorld.inf をダブルクリックします。 ハードウェア ID は \[Standard.NT$ARCH$\] の下に記載されています。

    ```C++
    [Standard.NT$ARCH$]
    %KmdfHelloWorld.DeviceDesc%=KmdfHelloWorld_Device, Root\KmdfHelloWorld
    ```

8. **[ビルド]** メニューで、 **[ソリューションの配置]** を選択します。 Visual Studio は、ドライバーのインストールと実行に必要なファイルを対象のコンピューターに自動的にコピーします。 この処理には 1 ～ 2 分かかる可能性があります。

    ドライバーを展開すると、テスト コンピューターの %Systemdrive%\drivertest\drivers フォルダーにドライバー ファイルがコピーされます。 展開中に何か異変に気付いた場合は、テスト コンピューターにファイルがコピーされているかどうかを確認してください。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\drivertest\drivers フォルダーに存在することを確認します。

    ドライバーの展開の詳細については、「[テスト コンピューターへのドライバーの展開](../develop/deploying-a-driver-to-a-test-computer.md)」を参照してください。

## <a name="install-the-driver"></a>ドライバーのインストール

対象のコンピューターに Hello World ドライバーが展開されたので、次にドライバーをインストールします。 以前に Visual Studio で*自動*オプションを使用して対象のコンピューターをプロビジョニングした場合は、Visual Studio が対象のコンピューターがテスト署名されたドライバーをプロビジョニング プロセスの一部として実行するように設定します。 ここでは、DevCon ツールを使用してドライバーをインストールするだけです。

1. ホスト コンピューターで WDK インストール内の Tools フォルダーに移動し、DevCon ツールを見つけます。 たとえば、次のフォルダーを探します。

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

    DevCon ツールをリモート コンピューターにコピーします。

2. 対象のコンピューターでは、ドライバー ファイルを含むフォルダーに移動し、DevCon ツールを実行してドライバーをインストールします。 
    1. ここで示しているのは、ドライバーのインストールに使う devcon ツールの一般的な構文です。

        *devcon install \<INF ファイル\> \<ハードウェア ID\>*

        このドライバーのインストールに必要な INF ファイルは KmdfHelloWorld.inf です。 この INF ファイルには、ドライバーのバイナリ *KmdfHelloWorld.sys* のインストールに必要なハードウェア ID が含まれています。 INF ファイルにあるハードウェア ID が **Root\\KmdfHelloWorld** であることを思い出してください。
    2. 管理者としてコマンド プロンプト ウィンドウを開きます。 ビルドされたドライバーの .sys ファイルを含むフォルダーに移動し、次のコマンドを入力します。

        **devcon install kmdfhelloworld.inf root\\kmdfhelloworld**

        *devcon* が認識されないというエラー メッセージが表示された場合は、*devcon* ツールへのパスを追加してみてください。 たとえば、ターゲットコンピューター上の *C:\\Tools* という名前のフォルダーにコピーする場合は、次のコマンドを使ってみてください。

        **c:\\tools\\devcon install kmdfhelloworld.inf root\kmdfhelloworld**

        ダイアログ ボックスには、テスト ドライバーが署名されていないドライバーであることが示されます。 **[かまわず続行]** をクリックして続行します。

        ![ドライバーのインストールに関する警告のスクリーン ショット](../debugger/images/debuglab-image-install-security-warning.png)

## <a name="debug-the-driver"></a>ドライバーのデバッグ

対象のコンピューターに KmdfHelloWorld ドライバーをインストールしたので、ホスト コンピューターからリモートでデバッガーをアタッチします。

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 WinDbg.exe ディレクトリに移動します。 Windows キットの一部としてインストールされた Windows Driver Kit (WDK) に含まれる WinDbg.exe の x64 バージョンを使います。 WinDbg.exe の既定のパスを次に示します。

    *C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64*

2. 次のコマンドを使用して、対象のコンピューターで WinDbg を起動してカーネル デバッグ セッションに接続します。 ポートとキーの値は、対象のコンピューターをプロビジョニングするために使用したものと同じである必要があります。 ポートに **50000**、キーに **1.2.3.4** を使用します。これは展開の手順で使用した値です。 *k* フラグは、これがカーネル デバッグ セッションであることを示します。

    **WinDbg -k net:port=50000,key=1.2.3.4**

3.  **[デバッグ]** メニューの **[中断]** をクリックします。 ホスト コンピューター上のデバッガーが、ターゲット コンピューターに割り込みます。 **デバッガーのコマンド** ウィンドウに、カーネルのデバッグ コマンド プロンプト **kd\>** が表示されます。

4. この段階で、**kd&gt;** プロンプトに対してコマンドを入力することにより、デバッガーの操作を試してみることができます。 たとえば、次のようなコマンドを試すことができます。

    -   [lm](https://go.microsoft.com/fwlink/p?linkid=399236)
    -   [.sympath](https://go.microsoft.com/fwlink/p?linkid=399238)
    -   [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)
    -   [x KmdfHelloWorld!\*](https://go.microsoft.com/fwlink/p?linkid=399240)

5. 対象のコンピューターを再び実行するには、 **[デバッグ]** メニューの **[続行]** をクリックするか、または "g" を押してから、Enter キーを押します。
6. デバッグ セッションを停止するには、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

    > [!IMPORTANT]
    > "go" コマンドを使用して、デバッガーを終了する前に対象のコンピューターをもう一度実行するようにしてください。そうしないと、対象のコンピューターがまだデバッガーとやり取りをしている状態であるため、マウスとキーボード入力に応答しないままになります。

ドライバー デバッグ プロセスの詳細な手順については、「[ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)」を参照してください。

リモート デバッグの詳細については、「[WinDbg を使用したリモート デバッグ](../debugger/remode-debugging-using-windbg.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[ドライバーの開発、テスト、および展開](https://go.microsoft.com/fwlink/p?linkid=399234)

[Windows 用デバッグ ツール](https://go.microsoft.com/fwlink/p?linkid=223405)

[ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)

[初めてのドライバーの作成](writing-your-first-driver.md)
