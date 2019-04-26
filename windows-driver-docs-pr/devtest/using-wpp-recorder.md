---
title: ログ トレースのように、転送トレース レコーダー (IFR)
description: 転送トレース レコーダー (IFR) は、トレースなど、プロバイダーをカーネル モード ドライバーでは、最小限の設定でトレース ログを取得し、一連の最新の WPP ログ メッセージが保持されます、インメモリ バッファーを作成することができる新しいトレース機能です。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7df66cfc6e9ff645171ad8563e0caf86daaf68f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358935"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>ログ トレースのように、転送トレース レコーダー (IFR)


**概要**

-   Visual Studio での転送トレース レコーダーを有効にする方法
-   WPP 既定のログまたはカスタムのログにトレース メッセージを送信する方法
-   デバッガーでのトレース メッセージを表示する方法

**適用対象:**

-   最小 OS:WDM、KMDF ドライバー開発者向け Windows 8
-   最小 OS:(2.15) UMDF ドライバー開発者向け Windows 10

**重要な API**

-   [**WppRecorderLogGetDefault**](https://msdn.microsoft.com/library/windows/hardware/dn895240)
-   [**WppRecorderLogCreate (カーネル モード ドライバーのみ)**](https://msdn.microsoft.com/library/windows/hardware/dn914615)
-   [**WppRecorderDumpLiveDriverData**](https://msdn.microsoft.com/library/windows/hardware/dn914612)

*転送トレース レコーダー (IFR)* はトレースなど、プロバイダーをカーネル モード ドライバーでは、最小限の設定でトレース ログを取得し、一連の最新の WPP ログ メッセージが保持されます、インメモリ バッファーを作成することができる、新しいトレース機能です。

Windows では、トレース メッセージを診断し、開発中には、ドライバーの問題をデバッグすることができるドライバーを追加するためのいくつかのメカニズムを提供します。 このような 1 つのメカニズムは[WPP ソフトウェア トレース](wpp-software-tracing.md)します。 含まれています、 [WPP プリプロセッサ](wpp-preprocessor.md)printf スタイルのトレース メッセージを小さいメモリ フット プリントを持つトレース プロバイダーをできるようにします。 ただし、トレース メッセージのログを表示するには、プロバイダーがありますなどを有効に、トレース コントローラ[traceview で](traceview.md)または[Tracelog](tracelog.md)停止し、ログ、および次に、コンシューマーを作成するには、トレース セッションを開始する必要がありますなど、traceview では、書式設定し、ログを表示する必要があります。

Windows 10 には、新しい機能が導入されています。WPP インフラストラクチャを活用して IFR します。 ドライバーは、WPP トレースと IFR により、トレース ログを自動的に有効にし、起動またはトレース セッションを停止せずに簡単にメッセージを表示できます。

IFR ドライバーの場合と呼ばれる非ページ プールからメモリの 1 つのページを割り当て、*既定のログ*します。 ログは、ドライバーによって送信されるトレース メッセージを収集し、ドライバーを実行すると、カーネル デバッガーで、バッファーの出力を表示できます。 クラッシュが発生した場合は、ダンプに最新のトレース メッセージを取得できます。 トレース データを収集するクラッシュを再構築する必要はありません。

ドライバーが最小構成でトレース ログを取得するために主に、既定のログの使用をお勧めします。 ドライバーに既定のログのサイズを制御がないことに注意してください。 すべてのトレース メッセージは、1 つの循環バッファが送信されるため、最新のメッセージは情報のレベルに関係なく、以前のメッセージを上書きします。 場合によっては、エラー メッセージがないし、情報メッセージだけを確認できます。

ログはより詳細にコントロールを取得するには、IFR はカスタム バッファー作成および管理するためのドライバーを許可します。

**注**のみのカーネル モード ドライバー (KMDF および WDM)、Windows のこのリリースでカスタムのバッファーを作成できます。 UMDF ドライバーでは、カスタムのバッファーを作成できません。



-   ドライバーは、verbose ロガーは、バッファーをあふれしないように、さまざまな目的は、複数のバッファーを作成できます。
-   ドライバーは、カスタムのバッファーとカスタムのバッファーのエラー パーティション (後述) のサイズを制御できます。
-   ドライバーは、カスタム ログの文字列識別子を指定できます。 トレース メッセージを表示するには、中に別のバッファーからメッセージを区別することができます。
-   WPP のメッセージを表示するには IFR がドライバーを有効になっている IFR を使用しても、WPP 上に構築されたため、 [traceview で](traceview.md)します。 ただし、それらのメッセージを表示するには、トレース プロバイダーを有効にしてセッションを開始する必要があります。

**重要**  
IFR 内のメッセージには、それらに関連付けられているタイムスタンプはありません。

トレース メッセージは、Windows デバッガーでのみ表示できます。



## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin..."></span><span id="before_you_begin..."></span><span id="BEFORE_YOU_BEGIN..."></span>開始する前にしています.


-   理解して[WPP ソフトウェア トレース](wpp-software-tracing.md)など[WPP ソフトウェア トレースを追加するには、ドライバーを](adding-wpp-software-tracing-to-a-windows-driver.md)と[WPP マクロを呼び出すことの宣言と](adding-wpp-macros-to-a-trace-provider.md)します。
-   このブログ記事については、[を含めるし、ドライバーのパブリックの PDB ファイルに WPP トレース メッセージを表示する方法](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)します。
-   トースター サンプルを検討します。 IFR を有効にして、それを使用する方法を示すために変更されました。 詳細については、次を参照してください。[トースター サンプル ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=617723)します。

## <a name="span-idenablewppsoftwaretracingspanspan-idenablewppsoftwaretracingspanspan-idenablewppsoftwaretracingspanenable-wpp-software-tracing"></a><span id="Enable_WPP_software_tracing"></span><span id="enable_wpp_software_tracing"></span><span id="ENABLE_WPP_SOFTWARE_TRACING"></span>WPP ソフトウェア トレースを有効にします。


IFR を使用するには、ドライバーを構成する前に、WPP としてドライバーを設定する必要があります最初する[トレース プロバイダー](trace-provider.md)します。

-   Visual Studio で提供される WDF ドライバー テンプレートを使用して、ドライバーを作成する場合は、WPP トレースが有効にします。 プロジェクトのプロパティで、トレース関連の設定を表示します。

    1.  Visual Studio では、ソリューション エクスプ ローラーで有効にし、をクリックするプロジェクトを右クリックして**プロパティ。**
    2.  (たとえば、すべての構成とすべてのプラットフォーム) をサポートするビルド ターゲットを構成およびプラットフォームを設定します。
    3.  プロジェクト プロパティ ページで、選択**構成プロパティ**クリック**WPP トレース**します。
    4.  **全般**、 をクリックして**Wpp トレースの実行**を選択します**はい** をクリックし、ドロップダウン メニューから**ok**します。

        ![visual studio で、wpp ソフトウェア トレースを有効にします。](images/wpp-enable.png)

    5.  **ファイル オプション**の値を設定**構成データのスキャン**を含むトレース情報ファイルの名前に、デバッグ関連の関数定義とマクロをトレースします。 この例で、定義は Trace.h です。

        ![visual studio で、wpp ソフトウェア トレースを有効にします。](images/wpp-enable2.png)

-   WDF のドライバー テンプレートのいずれかを使用されていない場合、は、WPP ソフトウェア トレースを設定します。 ヘッダー ファイル (WDF テンプレートで提供される trace.h に類似) を作成します。 ヘッダー ファイルには、WPP マクロが含まれています ([WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)、 [WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)) と WPP 制御フラグとトレース メッセージのステートメント。 手順については、次を参照してください。 [Windows ドライバーに WPP ソフトウェア トレースを追加する](adding-wpp-software-tracing-to-a-windows-driver.md)します。

    これらのタスクを実行することを確認します。

    -   トレース プロバイダーとして、ドライバーの GUID を定義します。

        **WPP 構文\_コントロール\_GUID**

        ```ManagedCPlusPlus
        #define WPP_CONTROL_GUIDS \
            WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
                WPP_DEFINE_BIT(NameOfTraceFlag1)  \
                WPP_DEFINE_BIT(NameOfTraceFlag2)  \
                .............................   \
                .............................   \
                WPP_DEFINE_BIT(NameOfTraceFlag31) 
        ```

    -   トレース ステートメントを印刷するソース ファイルには、(この例では、Trace.h) では、トレースのヘッダー ファイルを含めます。
    -   含める[トレース メッセージの形式](trace-message-format-file.md)、ソース ファイルに関連付けられているファイル (*&lt;ソース ファイル&gt;*.tmh) を出力するトレース メッセージを含むソース ファイル。
        ```ManagedCPlusPlus
        #include "trace.h"
        //
        // This tmh is generated by the WPP Preprocessor.
        //
        #include "MyDriver.tmh"
        ```

    -   初期化の WPP [DriverEntry](28131-driverentry-saving-pointer-to-buffer.md)ドライバーの。
        ```ManagedCPlusPlus
        //
        // WPP Initialization
        //
        WPP_INIT_TRACING(DriverObject, RegistryPath);

        ```

    -   ドライバー、unload メソッドでの WPP リソースを解放します。
        ```ManagedCPlusPlus
        //
        // WPP release resources
        //

        WPP_CLEANUP( DriverObject) );
        ```

## <a name="span-idstep2spanspan-idstep2spanenable-ifr"></a><span id="step_2"></span><span id="STEP_2"></span>IFR を有効にします。


WPP ソフトウェア トレースをドライバーを追加した後、IFR インフラストラクチャが既に配置します。 プロジェクトのプロパティの機能を有効にする必要があるだけです。

1.  Visual Studio では、ソリューション エクスプ ローラーで有効にし、をクリックするプロジェクトを右クリックして**プロパティ。**
2.  (たとえば、すべての構成とすべてのプラットフォーム) をサポートするビルド ターゲットを構成およびプラットフォームを設定します。
3.  プロジェクトのプロパティ ページで次のようにクリックします。**構成プロパティ**クリック**WPP トレース**。
4.  **関数とマクロ オプション**、 をクリックして**WPP レコーダーを有効にする**を選択します**はい** をクリックし、ドロップダウン メニューから**ok**します。

    これを定義、**を有効にする\_WPP\_レコーダー**コンパイラ フラグも有効にする DLL のマクロを設定し、(**-dll** UMDF ドライバーと**km** kmdfドライバーの場合)。

    有効になっている, 違いますを使用しても WPP メッセージは引き続き、Windows Driver Kit (WDK) で含まれている traceview でなどのツールを使用して、IFR を使用せず記録されます。

    ![visual studio で wpp レコーダーを有効にします。](images/wpp-enable3.png)

5.  WppRecorder.lib とドライバーのプロジェクトをリンクします。

    1.  プロジェクトのプロパティ をクリックして**構成プロパティ**クリック**リンカー**します。
    2.  **入力**、追加 **$(DDK\_LIB\_パス)\\wpprecorder.lib**を**追加の依存関係**フィールド。

    ![visual studio で wpp レコーダーを有効にします。](images/wpp-enable4.png)

6.  追加**Wpprecorder.h**を各ソース ファイルなど、IFR Api の呼び出しに[ **WppRecorderLogCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn914615) IFR ログを設定します。 後の Api を呼び出す、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)呼び出し、 *DriverEntry* KMDF ドライバーまたは UMDF 2.15 ドライバーの日常的な。

## <a name="span-idusethedefaultlogspanspan-idusethedefaultlogspanspan-idusethedefaultlogspanuse-the-default-log"></a><span id="Use__the_default_log"></span><span id="use__the_default_log"></span><span id="USE__THE_DEFAULT_LOG"></span>既定のログを使用して、


ドライバーのプロジェクトで WPP を有効にした後、WPP は既定のログを作成します。 WPP を出力する既定のログのバッファー サイズは、4096 バイトです。 デバッグ ビルドでは、バッファーは、24576 バイトです。

既定のログ バッファーを割り当てることが失敗すると、トレース メッセージは、WPP に送信されます。 つまり、, 違いますでは、トレース メッセージは記録されませんが、トレースは、ライブ WPP トレースとしてまだ認識できます。 既定のログが作成されたかどうかを判断するドライバーを呼び出す必要があります[ **WppRecorderIsDefaultLogAvailable**](https://msdn.microsoft.com/library/windows/hardware/dn914614)します。 既定のログが存在しないドライバーが IFR を使用したい場合は、ドライバーは、ログを作成する必要があります。 詳細については、次を参照してください。[カスタム ログ作成](#create)です。

1.  初期化を[**レコーダー\_構成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914606)呼び出して構造[**レコーダー\_構成\_PARAMS\_INIT**](https://msdn.microsoft.com/library/windows/hardware/dn914607)します。 マクロのセット、 **CreateDefaultLog** true の場合、メンバー、ドライバーが既定のログを使用することを示します。
2.  呼び出す[ **WppRecorderConfigure** ](https://msdn.microsoft.com/library/windows/hardware/dn914611) 、初期化済みのアドレスを指定して[**レコーダー\_構成\_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/dn914606)構造体。
3.  レコーダーを取得する\_呼び出すことによって既定のログにログの非透過ハンドル[ **WppRecorderLogGetDefault**](https://msdn.microsoft.com/library/windows/hardware/dn895240)します。
4.  Trace.h で宣言されているトレース マクロを呼び出すことによって、既定のログにトレース メッセージを印刷します。 詳細については、次を参照してください。[トレース関数を定義](#define)します。
5.  ビューは、デバッガーでのメッセージをトレースします。 詳細については、次を参照してください。[トレース メッセージを表示](#view)します。

**注**既定のログを無効にする設定、 **CreateDefaultLog**のメンバー、 [**レコーダー\_構成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914606)にFalse の場合、まず[ **WppRecorderConfigure**](https://msdn.microsoft.com/library/windows/hardware/dn914611)します。



この例では、ドライバーは、既定のログを識別するハンドルを取得します。

```ManagedCPlusPlus

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG logHandle = NULL;

        // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);

    // If a default log is available, store the handle to the default log.

    if (WppRecorderIsDefaultLogAvailable())
    {
        RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

        WppRecorderConfigure(&recorderConfig);

        logHandle = WppRecorderLogGetDefault();

    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-idcreatespanspan-idcreatespancreate-a-custom-log-kernel-mode-drivers-only"></a><span id="create"></span><span id="CREATE"></span>カスタム ログ (カーネル モード ドライバーのみ) を作成します。


IFR に対する既定のログでは、非ページ プール メモリの 4096 ブロックを使用します。 すべてのトレース メッセージは、循環バッファーに書き込まれます。 最新のメッセージは、以前のメッセージを上書きできます。

たとえばには、ドライバーでは、コントロールとデータの転送要求の個別のフロー パスがあります。 両方からのアクティビティは、最も可能性の高い、同じバッファーにログインしている場合、コントロールにメッセージをトレースはデータの転送メッセージによって上書きされます。 この場合、それらの要求を別のバッファーを構成できます。

別の例である 2 つのデバイス、および 1 つのデバイスの送信よりも、その他の複数のトレース メッセージ。 ドライバーは、既定のログを使用している場合、バッファーがいっぱいになるデバイスなり、他のデバイスからのメッセージに削除できます。 代わりに、ドライバーは、各デバイスは、そのバッファーにメッセージを送信でき、各デバイスからのメッセージを個別に表示できるように、2 つのカスタム ログを作成できます。

1.  初期化を[**レコーダー\_ログ\_作成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914608)呼び出して構造[**レコーダー\_ログ\_作成\_PARAMS\_INIT**](https://msdn.microsoft.com/library/windows/hardware/dn914609)します。 構造体のメンバーが変更されていない限り、WPP は既定のログ パラメーターを使用します。
2.  任意。 設定、 **TotalBufferSize**目的のサイズにメンバー。 既定では、サイズが 1024 バイトに設定されます (レコーダーを参照してください。\_ログ\_既定\_バッファー\_Wpprecorder.h サイズ)。
    **注**WPP は、非ページ プールから、ログのバッファーを割り当てます。 ログはパーティションと呼ばれる 2 つの循環バッファに分かれています。 [全般]、エラー。 エラー パーティションのみのトレース メッセージが表示されます\_レベル\_エラー。 その他のすべてのレベルに関連するメッセージは、一般的なパーティションに送信されます。 パーティションは、詳細トレース プロバイダーが独自のエラー メッセージを低優先度のメッセージを上書きするを防ぐために設計されています。 呼び出し元のバッファー サイズを指定する**TotalBufferSize**、それらのパーティションの合計サイズを示します。 エラーのパーティションには、合計バッファー サイズの半分を超えることはできません。 初期化後に、バッファー サイズを変更できます。



3.  任意。 設定、 **LogIdentifier**をこのバッファーからのトレース メッセージを識別するのに役立つ文字列です。 文字列は、16 文字でを超えない必要があります。
4.  呼び出す[ **WppRecorderLogCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn914615)の設定されたアドレスを指定して[**レコーダー\_ログ\_作成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914608)構造体。
5.  この新しいバッファーへのトレース メッセージを印刷するには、トレース マクロを呼び出すと、レコーダーを渡す\_で受信したログのハンドル、 [ **WppRecorderLogCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn914615)を呼び出します。
6.  ビューは、デバッガーでのメッセージをトレースします。 詳細については、次を参照してください。[トレース メッセージを表示](#view)します。

システムでは、レジストリに最大と最小バッファー サイズを定義します。 メモリを節約し、ログ機能を構成するのには、これらの値を適切に設定できます。

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<serviceName>\Parameters
   WppRecorder_PerBufferMinBytes
   Data type
   REG_DWORD
   Description
   The minimum number of bytes that can be allocated to a  log buffer.  The default is 256 bytes.

   WppRecorder_PerBufferMaxBytes
   Data type
   REG_DWORD
   Description
   The maximum number of bytes that can be allocated to a  log buffer.  The default is 8192 bytes.

   LogPages
   Data type
   REG_DWORD
   Description
   The number of pages to store the default log. The default is 1.

   VerboseOn
   Data type
   REG_DWORD
   Description
   By default (0), IFR only logs errors, warnings, and informational events. Setting this value to 1 adds the verbose output to get logged. 
```

サイズが指定されている場合[**レコーダー\_ログ\_作成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914608) (バイト単位) の最小数未満[ **WppRecorderLogCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn914615)割り当てます**WppRecorder\_PerBufferMinBytes**バイト。 同様に、サイズが最大の値を超えた場合、 **WppRecorderLogCreate**割り当てます**WppRecorder\_PerBufferMaxBytes**バイト。

カスタム ログを削除する[ **WppRecorderLogDelete** ](https://msdn.microsoft.com/library/windows/hardware/dn914616)呼び出す前に[WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)します。 この関数を入力すると、スレッド、すべてのスレッドする必要がありますにログインしないこのバッファーできなくなります。 この関数を呼び出すことができます、 [ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)ドライバーの実装。

このコード例では、ドライバーの DriverEntry 関数からスニペットを示します。 この例で、ドライバーは既定のログを無効にします、カスタム ログを作成して、バッファー サイズ、および識別子を設定します。

```ManagedCPlusPlus
ULONG MyDriverLogSize = 8 * 1024;

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG_CREATE_PARAMS recorderCreate;

    RECORDER_LOG logHandle = NULL;

    // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);
    // If a default log is available, then configure the size of the buffer.
    // Store the handle to the default log and use it to set the identifier name.

    RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

    recorderConfig.CreateDefaultLog = FALSE;

    RECORDER_LOG_CREATE_PARAMS_INIT(&recorderCreate, NULL);
    recorderCreate.TotalBufferSize = MyDriverLogSize;
    RtlStringCbPrintfA(recorderCreate.LogIdentifier,
        RECORDER_LOG_IDENTIFIER_MAX_CHARS,
        "KMDFWpp_Log");

    status = WppRecorderLogCreate(&recorderCreate, &logHandle);
    if (!NT_SUCCESS(status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DRIVER, "WppRecorderLogCreate failed %!STATUS!", status);
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-iddefinespanspan-iddefinespandefine-trace-functions"></a><span id="define"></span><span id="DEFINE"></span>トレース関数を定義します。


入力パラメーターとして"IFRLOG"がある、Trace.h) の「トレース関数を追加します。 トレース マクロについては、次を参照してください。 [Windows ドライバーに追加の WPP ソフトウェア トレース](adding-wpp-software-tracing-to-a-windows-driver.md)します。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// end_wpp
//
```

前の例では、TraceEvents と PrintEvents の 2 つのトレース機能があります。 WPP は、FUNC 宣言で指定されたパラメーターと共にこれらの関数のマクロを生成します。 このトピックの「使用例ドライバーは、TraceEvents と PrintEvents の両方を使用します。 PrintEvents では、パラメーターとして"IFRLOG"が必要です。 この関数を呼び出すときに、ドライバーがレコーダーを指定する必要があります\_"IFRLOG"のパラメーター値としてログ ハンドル。 カスタムのバッファーを作成する場合にのみ、IFRLOG が追加されます。 TraceEvents は、既定のログを出力します。 これは、機能の変更を加えずに既存のトレース ステートメントとの下位互換性を提供します。

既定のログにトレース メッセージを印刷するには、ドライバーか呼び出し PrintEvents で受信したハンドルを持つ、 [ **WppRecorderLogGetDefault** ](https://msdn.microsoft.com/library/windows/hardware/dn895240)を呼び出すと、またはハンドルせず、TraceEvents に呼び出します。

カスタム ログに印刷するには、ドライバーはへの呼び出しで受け取ったハンドルを渡します。 [ **WppRecorderLogCreate**](https://msdn.microsoft.com/library/windows/hardware/dn914615)します。

## <a name="span-idmaketracemessagesavailableinpublicsymbolsspanspan-idmaketracemessagesavailableinpublicsymbolsspanspan-idmaketracemessagesavailableinpublicsymbolsspanmake-trace-messages-available-in-public-symbols"></a><span id="Make__trace_messages_available_in_public_symbols"></span><span id="make__trace_messages_available_in_public_symbols"></span><span id="MAKE__TRACE_MESSAGES_AVAILABLE_IN_PUBLIC_SYMBOLS"></span>トレース メッセージをパブリック シンボルで使用できるように


WPP[トレース メッセージの形式](trace-message-format-file.md)WPP の実際のメッセージを表示する情報が必要です。 その情報は、プライベート シンボル ファイル (Pdb) に格納されます。 TMF 情報は、プライベート PDB がパブリックの PDB されませんで自動的に含まれます。 そのため、プライベート PDB なし、メッセージを表示することはできません。 トレース メッセージをパブリックの pdb ファイルに追加するには

WPP トレース メッセージの一部をパブリックにするには、各メッセージに特別なマーカーを追加する必要があります。 追加`// WPP_FLAGS(-public:<trace function name>)`Trace.h ファイル定義の後にします。 マーカーが表示されます、 **– パブリック**WPP コマンドラインに切り替えます。 スイッチが WPP プリプロセッサに追加されるため、保持できる&lt;funcName&gt;パブリック PDB ファイルに注釈をトレースします。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC Trace{FLAG=MYDRIVER_ALL_INFO}(LEVEL, MSG, ...);
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// WPP_FLAGS(-public:PrintEvents);
// end_wpp
//
```

## <a name="span-idviewspanspan-idviewspanview-the-trace-messages"></a><span id="view"></span><span id="VIEW"></span>トレース メッセージを表示します。


トレース メッセージを表示する使用[Wdfkd 拡張](https://msdn.microsoft.com/library/windows/hardware/ff551876)Windows デバッガーでします。 拡張機能コマンドは、Wdfkd.dll です。

1.  Wdfkd コマンドを読み込む、入力`.load Wdfkd.dll`デバッガーでします。
2.  これらのコマンドを使用すると、トレース メッセージを表示できます。

    [**!wdfkd.wdflogdump**](https://msdn.microsoft.com/library/windows/hardware/ff565805)

    [**!wdfkd.wdfcrashdump**](https://msdn.microsoft.com/library/windows/hardware/ff565682)

カーネル モード ドライバーを使用してトレース ログを表示できます[RCDRKD 拡張](https://msdn.microsoft.com/library/windows/hardware/hh920376)します。 これらのコマンドでは、ユーザー モード ドライバーを使用できません。

## <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>ベスト プラクティス


-   後 IFR Api を呼び出す、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)呼び出し、 *DriverEntry*またはカーネル モード ドライバーの日常的な*DLLMain*ルーチンUMDF 2.15 ドライバー。 グローバル ポリシーによってログ記録が無効の場合は、WPP を呼び出す\_INIT\_トレースはログ記録を有効にします。

-   場合[ **WppRecorderLogCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn914615)が失敗した呼び出しの NULL ハンドルを返します。 戻り値を無視する場合、選択できます**WppRecorderLogCreate** 、RECODER を使用して\_ログ ハンドル、WPP メッセージを出力します。

-   によって返されたハンドルは削除しないでください[ **WppRecorderLogGetDefault**](https://msdn.microsoft.com/library/windows/hardware/dn895240)します。 既定のログを無効にする設定、 **CreateDefaultLog**のメンバー [**レコーダー\_構成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/dn914606)を FALSE を呼び出して[**WppRecorderConfigure**](https://msdn.microsoft.com/library/windows/hardware/dn914611)します。

-   呼び出さない[ **WppRecorderLogSetIdentifier** ](https://msdn.microsoft.com/library/windows/hardware/dn895241)既定のログのハンドルを渡すことによって。 その操作は許可されません。

-   IFR バッファーは、非ページ プールから割り当てられます。 それらの割り当ての累積的効果は、特にフット プリントの小さいデバイスでの大幅なパフォーマンスの問題につながります。 要求のバッファー サイズが小さく、 [ **WppRecorderLogCreate**](https://msdn.microsoft.com/library/windows/hardware/dn914615)します。 また、ログ記録機能が不要である場合、既定のログを無効にします。

-   ログ バッファーのサイズを表示する、 [ **! wdfkd.wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)コマンド。 使用する場合[RCDRKD 拡張](https://msdn.microsoft.com/library/windows/hardware/hh920376)、サイズを表示するを使用し、 [ **! rcdrkd.rcdrloglist**](https://msdn.microsoft.com/library/windows/hardware/hh920383)

## <a name="span-idumdfandkmdfdifferencesspanspan-idumdfandkmdfdifferencesspanspan-idumdfandkmdfdifferencesspanumdf-and-kmdf-differences"></a><span id="UMDF_and_KMDF_differences"></span><span id="umdf_and_kmdf_differences"></span><span id="UMDF_AND_KMDF_DIFFERENCES"></span>UMDF および KMDF の違い


-   カーネル モード ドライバーだけでは、カスタムのバッファーを作成できます。 この機能は、ユーザー モード ドライバーには適用されません。
-   使用して、ユーザー モード ドライバーからのトレース ログを表示することはできません[RCDRKD 拡張](https://msdn.microsoft.com/library/windows/hardware/hh920376)します。 使用する必要があります[Wdfkd 拡張](https://msdn.microsoft.com/library/windows/hardware/ff551876)します。









