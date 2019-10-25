---
title: トレースログ用の inflight トレースレコーダー (IFR)
description: Inflight トレースレコーダー (IFR) は、カーネルモードドライバーなどのトレースプロバイダーが最小限のセットアップでトレースログを取得し、最新の WPP ログメッセージが保存されるメモリ内バッファーのセットを作成するための新しいトレース機能です。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3399d177ef7a801f9f81da3849a8d87193a16172
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839261"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>トレースログ用の inflight トレースレコーダー (IFR)


**まとめ**

-   Visual Studio で Inflight トレースレコーダーを有効にする方法
-   WPP の既定のログまたはカスタムログにトレースメッセージを送信する方法
-   デバッガーでトレースメッセージを表示する方法

**適用対象:**

-   最小 OS: KMDF および WDM ドライバー開発者向けの Windows 8
-   最小 OS: Windows 10 for UMDF (2.15) ドライバー開発者

**重要な Api**

-   [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))
-   [**WppRecorderLogCreate (カーネルモードドライバーのみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)
-   [**WppRecorderDumpLiveDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

*Inflight トレースレコーダー (IFR)* は、カーネルモードドライバーなどのトレースプロバイダーが最小限のセットアップでトレースログを取得し、最新の WPP ログメッセージが保存されるメモリ内バッファーのセットを作成するための新しいトレース機能です。

Windows には、ドライバーにトレースメッセージを追加するためのいくつかのメカニズムが用意されており、開発時にドライバーの問題を診断してデバッグするのに役立ちます。 このようなメカニズムの1つは、 [WPP ソフトウェアのトレース](wpp-software-tracing.md)です。 これには、メモリフットプリントが小さい printf 形式のトレースメッセージをトレースプロバイダーに許可するための、 [WPP プリプロセッサ](wpp-preprocessor.md)が含まれています。 ただし、トレースメッセージのログを表示するには、プロバイダーが有効になっている必要があります。トレース[ビュー](traceview.md)やトレース[ログ](tracelog.md)などのトレースコントローラーは、ログを作成するためにトレースセッションを停止して起動する必要があります。その後、traceview などのコンシューマーが書式設定して表示する必要があります。ログ。

Windows 10 では、WPP インフラストラクチャを活用する新しい機能である IFR が導入されています。 ドライバーで WPP トレースと IFR が有効になっている場合は、トレースログが自動的に有効になり、トレースセッションを開始または停止しなくてもメッセージを簡単に表示できます。

IFR は、*既定のログ*と呼ばれる、ドライバーの非ページプールからメモリの1ページを割り当てます。 このログは、ドライバーによって送信されたトレースメッセージを収集し、ドライバーの実行時にカーネルデバッガーでバッファーの出力を表示できます。 クラッシュが発生した場合は、最新のトレースメッセージをダンプで取得できます。 トレースデータを収集するためだけにクラッシュを再構築する必要はありません。

既定のログは主に、ドライバーが最小構成でトレースログを取得できることが原因です。 ドライバーは、既定のログのサイズを制御できないことに注意してください。 すべてのトレースメッセージは1つの循環バッファーに送信されるため、最新のメッセージは、情報のレベルに関係なく、以前のメッセージを上書きします。 場合によっては、エラーメッセージを見逃すことがあり、情報メッセージのみが表示されます。

ログの制御を強化するために、IFR ではドライバーがカスタムバッファーを作成および管理することができます。

**メモ** このリリースの Windows では、カーネルモードドライバー (KMDF と WDM) のみがカスタムバッファーを作成できます。 UMDF ドライバーはカスタムバッファーを作成できません。



-   ドライバーは、さまざまな目的で複数のバッファーを作成できます。そのため、詳細ロガーはバッファーをオーバーフローしません。
-   ドライバーはカスタムバッファーのサイズとエラーパーティション (後で説明します) を制御できます。
-   ドライバーは、カスタムログの文字列識別子を指定できます。 トレースメッセージを表示している間に、異なるバッファーのメッセージを区別できます。
-   IFR は、ドライバーに対して IFR が有効になっている場合でも、WPP を基に構築されているため、 [traceview](traceview.md)で WPP メッセージを表示できます。 ただし、これらのメッセージを表示するには、トレースプロバイダーを有効にし、セッションを開始する必要があります。

**重要**  
IFR のメッセージにはタイムスタンプが関連付けられていません。

トレースメッセージは、Windows デバッガーでのみ表示できます。



## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin..."></span><span id="before_you_begin..."></span><span id="BEFORE_YOU_BEGIN..."></span>開始する前に...


-   Wpp ソフトウェアトレースの[ドライバーへの追加](adding-wpp-software-tracing-to-a-windows-driver.md)や、 [wpp マクロの宣言と呼び出し](adding-wpp-macros-to-a-trace-provider.md)など、 [wpp ソフトウェアトレース](wpp-software-tracing.md)について理解を深めます。
-   このブログ記事では、[ドライバーのパブリック PDB ファイルに WPP トレースメッセージを含める方法と表示する方法](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)について説明します。
-   トースターサンプルを調べます。 これは、IFR を有効にして使用する方法を示すために変更されています。 詳細については、「[トースター Sample Driver](https://go.microsoft.com/fwlink/p/?LinkId=617723)」を参照してください。

## <a name="span-idenable_wpp_software_tracingspanspan-idenable_wpp_software_tracingspanspan-idenable_wpp_software_tracingspanenable-wpp-software-tracing"></a><span id="Enable_WPP_software_tracing"></span><span id="enable_wpp_software_tracing"></span><span id="ENABLE_WPP_SOFTWARE_TRACING"></span>WPP ソフトウェアのトレースを有効にする


IFR を使用するようにドライバーを構成する前に、まず、ドライバーを WPP[トレースプロバイダー](trace-provider.md)として設定する必要があります。

-   Visual Studio に用意されている WDF ドライバーテンプレートを使用してドライバーを作成した場合、WPP トレースが有効になります。 トレース関連の設定は、プロジェクトのプロパティで確認できます。

    1.  Visual Studio で、ソリューションエクスプローラーで有効にするプロジェクトを右クリックし、[プロパティ] をクリックし**ます。**
    2.  構成とプラットフォームを、サポートするビルドターゲット ([すべての構成] や [すべてのプラットフォーム] など) に設定します。
    3.  プロジェクトのプロパティページで、 **[構成プロパティ]** を選択し、 **[WPP トレース]** をクリックします。
    4.  **[全般]** で、 **[Wpp トレースの実行]** をクリックし、ドロップダウンメニューの **[はい]** をクリックして、[ **OK]** をクリックします。

        ![visual studio での wpp ソフトウェアトレースの有効化](images/wpp-enable.png)

    5.  **[ファイルオプション]** で、 **[スキャン構成データ]** の値を、デバッグトレースに関連する関数の定義とマクロを含むトレース情報ファイルの名前に設定します。 この例では、定義は Trace. h にあります。

        ![visual studio での wpp ソフトウェアトレースの有効化](images/wpp-enable2.png)

-   WDF driver テンプレートのいずれかを使用していない場合は、WPP ソフトウェアのトレースを設定します。 ヘッダーファイルを作成します (WDF テンプレートで提供されているトレースに似ています)。 このヘッダーファイルには、WPP マクロ ([wpp\_INIT\_TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))、 [wpp\_CLEANUP](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85)))、および wpp 制御フラグとトレースメッセージステートメントが含まれています。 手順については、「 [Windows ドライバーへの WPP ソフトウェアトレースの追加](adding-wpp-software-tracing-to-a-windows-driver.md)」を参照してください。

    次のタスクを実行していることを確認します。

    -   ドライバーの GUID をトレースプロバイダーとして定義します。

        **WPP\_制御\_GUID の構文**

        ```ManagedCPlusPlus
        #define WPP_CONTROL_GUIDS \
            WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
                WPP_DEFINE_BIT(NameOfTraceFlag1)  \
                WPP_DEFINE_BIT(NameOfTraceFlag2)  \
                .............................   \
                .............................   \
                WPP_DEFINE_BIT(NameOfTraceFlag31) 
        ```

    -   トレースステートメントを出力するソースファイルにトレースヘッダーファイル (この例では、Trace .h) を含めます。
    -   出力するトレースメッセージが格納されているソースファイルに、ソースファイルに関連付けられている[トレースメッセージフォーマット](trace-message-format-file.md)ファイル ( *&lt;ソースファイル&gt;* tmh) を含めます。
        ```ManagedCPlusPlus
        #include "trace.h"
        //
        // This tmh is generated by the WPP Preprocessor.
        //
        #include "MyDriver.tmh"
        ```

    -   ドライバーの[Driverentry](28131-driverentry-saving-pointer-to-buffer.md)で、WPP を初期化します。
        ```ManagedCPlusPlus
        //
        // WPP Initialization
        //
        WPP_INIT_TRACING(DriverObject, RegistryPath);

        ```

    -   ドライバーのアンロード方法で、WPP リソースを解放します。
        ```ManagedCPlusPlus
        //
        // WPP release resources
        //

        WPP_CLEANUP( DriverObject) );
        ```

## <a name="span-idstep_2spanspan-idstep_2spanenable-ifr"></a><span id="step_2"></span><span id="STEP_2"></span>IFR を有効にする


ドライバーに WPP ソフトウェアトレースを追加した後、IFR インフラストラクチャは既に配置されています。 プロジェクトのプロパティでのみ機能を有効にする必要があります。

1.  Visual Studio で、ソリューションエクスプローラーで有効にするプロジェクトを右クリックし、[プロパティ] をクリックし**ます。**
2.  構成とプラットフォームを、サポートするビルドターゲット ([すべての構成] や [すべてのプラットフォーム] など) に設定します。
3.  プロジェクトのプロパティページで、 **[構成プロパティ]** をクリックし、 **[WPP トレース]** をクリックします。
4.  **[関数とマクロのオプション]** で、 **[WPP レコーダーを有効にする]** をクリックし、ドロップダウンメニューの **[はい]** をクリックして、[ **OK]** をクリックします。

    これ**により、enable\_WPP\_レコーダー**コンパイラフラグが定義されます。また、enable dll マクロ (UMDF ドライバーの場合は **-DLL** 、kmdf ドライバーの場合は **-km** ) も設定されます。

    IFR が有効になっている場合でも、Windows Driver Kit (WDK) に含まれる Traceview などのツールを使用して、IFR を使用しなくても、WPP メッセージを記録できます。

    ![visual studio での wpp レコーダーの有効化](images/wpp-enable3.png)

5.  ドライバープロジェクトを WppRecorder にリンクします。

    1.  プロジェクトのプロパティ で、**構成プロパティ** をクリックし、**リンカー** をクリックします。
    2.  **[入力]** で、 **[追加の依存関係]** フィールドに **$ (DDK\_lib\_PATH)\\** 追加します。

    ![visual studio での wpp レコーダーの有効化](images/wpp-enable4.png)

6.  独自の IFR ログを設定する[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)など、ifr api を呼び出す各ソースファイルに**wpprecorder**を追加します。 KMDF または UMDF 2.15 ドライバーの*Driverentry*ルーチンで、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))呼び出しの後に api を呼び出します。

## <a name="span-iduse__the_default_logspanspan-iduse__the_default_logspanspan-iduse__the_default_logspanuse-the-default-log"></a><span id="Use__the_default_log"></span><span id="use__the_default_log"></span><span id="USE__THE_DEFAULT_LOG"></span>既定のログを使用する


WPP がドライバープロジェクトに対して有効になると、WPP によって既定のログが作成されます。 WPP が出力する既定のログのバッファーサイズは4096バイトです。 デバッグビルドの場合、バッファーは24576バイトです。

既定のログバッファーの割り当てに失敗すると、トレースメッセージが WPP に送信されます。 つまり、トレースメッセージは IFR では記録されませんが、トレースはライブ WPP トレースとして表示される可能性があります。 既定のログが作成されたかどうかを確認するには、ドライバーは[**WppRecorderIsDefaultLogAvailable**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn914614(v=vs.85))を呼び出す必要があります。 既定のログが存在せず、ドライバーが IFR を使用する必要がある場合、ドライバーはログを作成する必要があります。 詳細については、「[カスタムログを作成する](#create)」を参照してください。

1.  レコーダーを呼び出すことによって[ **\_params 構造を構成\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)には、レコーダーを初期化し[ **\_\_params\_INIT を構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-recorder_configure_params_init)します。 マクロは**Createdefaultlog**メンバーを TRUE に設定します。これは、ドライバーが既定のログを使用することを示します。
2.  初期化されたレコーダーのアドレスを指定して[**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)を呼び出し、\_PARAMS 構造体を[**構成\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)ます。
3.  [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))を呼び出すことにより、既定のログへの非透過的ハンドルをログに記録\_レコーダーを取得できます。
4.  トレースメッセージを既定のログに出力するには、trace で宣言されたトレースマクロを呼び出します。 詳細については、「 [Define trace functions](#define)」を参照してください。
5.  デバッガーでトレースメッセージを表示します。 詳細については、「[トレースメッセージの表示](#view)」を参照してください。

**メモ** 既定のログを無効にするには、レコーダーの**Createdefaultlog**メンバー [ **\_\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)を FALSE に設定してから、 [**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)を呼び出します。



この例では、ドライバーは既定のログへのハンドルを取得します。

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

## <a name="span-idcreatespanspan-idcreatespancreate-a-custom-log-kernel-mode-drivers-only"></a><span id="create"></span><span id="CREATE"></span>カスタムログを作成する (カーネルモードドライバーのみ)


IFR の既定のログでは、非ページプールメモリの4096ブロックが使用されます。 すべてのトレースメッセージは、循環バッファーに書き込まれます。 場合によっては、最新のメッセージによって前のメッセージが上書きされることがあります。

たとえば、ドライバーには、制御およびデータ転送要求用の個別のフローパスがあります。 両方のアクティビティが同じバッファーに記録された場合、ほとんどの場合、コントロールトレースメッセージはデータ転送メッセージによって上書きされます。 この場合は、これらの要求に対して個別のバッファーを構成できます。

別の例では、2つのデバイスがあり、1つのデバイスが他より多くのトレースメッセージを送信します。 ドライバーが既定のログを使用する場合、そのデバイスはバッファーをあふれさせることができ、他のデバイスからのメッセージは破棄される可能性があります。 代わりに、ドライバーは、各デバイスがバッファーにメッセージを送信できるように、2つのカスタムログを作成できます。また、各デバイスからのメッセージを個別に表示することもできます。

1.  レコーダー\_LOG を呼び出して[ **\_params 構造を作成\_\_ログ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)を初期化し\_[**params\_INIT を作成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-recorder_log_create_params_init)します。\_ WPP は、構造体のメンバーが変更されない限り、既定のログパラメーターを使用します。
2.  省略可能。 **Totalbuffersize**メンバーを目的のサイズに設定します。 既定では、サイズは1024バイトに設定されています (「レコーダー\_LOG\_既定の\_バッファー\_サイズ」を参照してください)。
    **メモ** WPP は、非ページプールからログのバッファーを割り当てます。 ログは、パーティション (general と error) と呼ばれる2つの循環バッファーに分割されます。 エラーパーティションには、トレース\_レベル\_エラーのメッセージのみが表示されます。 他のすべてのレベルに関連するメッセージは、一般パーティションに送信されます。 パーティションは、詳細トレースプロバイダーが、優先度の低いメッセージで独自のエラーメッセージを上書きしないように設計されています。 呼び出し元は、これらのパーティションの合計サイズを示す**Totalbuffersize**のバッファーサイズを指定します。 エラーパーティションは、合計バッファーサイズの半分を超えることはできません。 バッファーサイズは、初期化後に変更できます。



3.  省略可能。 **Logidentifier**には、このバッファーからのトレースメッセージを識別するのに役立つ文字列を設定します。 文字列の長さは16文字以下でなければなりません。
4.  入力した[**レコーダー\_ログ\_作成\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)構造体のアドレスを指定して、 [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)を呼び出します。
5.  トレースマクロを呼び出し、 [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)呼び出しによって受信されたレコーダー\_ログハンドルを渡すことによって、この新しいバッファーにトレースメッセージを出力します。
6.  デバッガーでトレースメッセージを表示します。 詳細については、「[トレースメッセージの表示](#view)」を参照してください。

システムは、レジストリの最大バッファーサイズと最小バッファーサイズを定義します。 これらの値は、メモリを節約し、ログ記録機能を構成するために適切に設定できます。

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

[**レコーダー\_LOG\_CREATE\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)が最小バイト数未満の場合は、 [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)によって**Wpprecorder\_perbufferminbytes**バイトが割り当てられます。 同様に、サイズが最大値を超えた場合、 **WppRecorderLogCreate**は**wpprecorder\_perbuffermaxbytes**バイトに割り当てます。

カスタムログを削除するには、 [**WppRecorderLogDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogdelete)を呼び出してから、 [WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))を呼び出します。 スレッドがこの関数に入ると、すべてのスレッドがこのバッファーにログインできなくなります。 この関数は、ドライバーの[*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)実装で呼び出すことができます。

このコード例は、ドライバーの DriverEntry 関数のスニペットです。 この例では、ドライバーは既定のログを無効にし、カスタムログを作成して、そのバッファーサイズと識別子を設定します。

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

## <a name="span-iddefinespanspan-iddefinespandefine-trace-functions"></a><span id="define"></span><span id="DEFINE"></span>トレース関数を定義する


"IFRLOG" を入力パラメーターとして持つトレース関数 (トレース .h 内) を追加します。 マクロのトレースの詳細については、「 [Windows ドライバーへの WPP ソフトウェアトレースの追加](adding-wpp-software-tracing-to-a-windows-driver.md)」を参照してください。

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

前の例では、TraceEvents と PrintEvents という2つのトレース関数があります。 WPP は、FUNC 宣言で指定されたパラメーターを使用して、これらの関数のマクロを生成します。 このトピックで使用する例では、ドライバーは TraceEvents と PrintEvents の両方を使用します。 PrintEvents には、パラメーターとして "IFRLOG" が必要です。 この関数を呼び出す場合、ドライバーは、"IFRLOG" のパラメーター値としてレコーダー\_ログハンドルを指定する必要があります。 IFRLOG は、カスタムバッファーを作成した場合にのみ追加されます。 TraceEvents は既定のログに出力します。 これにより、機能を変更することなく、既存のトレースステートメントとの下位互換性が提供されます。

トレースメッセージを既定のログに出力するには、ドライバーは、 [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))呼び出しで受信したハンドルを使用して printevents を呼び出すか、ハンドルなしで traceevents を呼び出します。

カスタムログに出力するために、ドライバーは、 [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)への呼び出しで受信したハンドルを渡します。

## <a name="span-idmake__trace_messages_available_in_public_symbolsspanspan-idmake__trace_messages_available_in_public_symbolsspanspan-idmake__trace_messages_available_in_public_symbolsspanmake-trace-messages-available-in-public-symbols"></a><span id="Make__trace_messages_available_in_public_symbols"></span><span id="make__trace_messages_available_in_public_symbols"></span><span id="MAKE__TRACE_MESSAGES_AVAILABLE_IN_PUBLIC_SYMBOLS"></span>トレースメッセージをパブリックシンボルで使用できるようにする


WPP では、実際の WPP メッセージを表示するために[トレースメッセージの形式](trace-message-format-file.md)情報が必要です。 この情報は、プライベートシンボルファイル (Pdb) に格納されます。 TMF 情報は、プライベート PDB に自動的に含まれますが、パブリック PDB には含まれません。 そのため、プライベート PDB を使用しないでメッセージを表示することはできません。 パブリック PDB にトレースメッセージを追加するには、

これらの WPP トレースメッセージの一部を公開するには、各メッセージに特別なマーカーを追加する必要があります。 トレース .h ファイルの定義の後に `// WPP_FLAGS(-public:<trace function name>)` を追加します。 マーカーは、WPP コマンドラインで **– public**スイッチによって示されます。 このスイッチを WPP プリプロセッサに追加して、&lt;funcName&gt; のトレース注釈をパブリック PDB ファイルに保持できるようにします。

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

## <a name="span-idviewspanspan-idviewspanview-the-trace-messages"></a><span id="view"></span><span id="VIEW"></span>トレースメッセージを表示する


トレースメッセージを表示するには、Windows デバッガーで[Wdfkd 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)を使用します。 拡張コマンドは、Wdfkd .dll です。

1.  Wdfkd コマンドを読み込み、デバッガーに `.load Wdfkd.dll` を入力します。
2.  これらのコマンドを使用して、トレースメッセージを表示します。

    [ **! wdfkd. wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)

    [ **! wdfkd。 wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)

カーネルモードドライバーは、 [Rcdrkd 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)を使用してトレースログを表示できます。 これらのコマンドは、ユーザーモードドライバーでは使用できません。

## <a name="span-idbest_practicesspanspan-idbest_practicesspanspan-idbest_practicesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>ベストプラクティス


-   カーネルモードドライバーの*Driverentry*ルーチン、または UMDF 2.15 ドライバーの*DLLMain*ルーチンで、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))呼び出しの開始後に、IFR api を呼び出します。 グローバルポリシーによってログ記録が無効になっている場合、WPP\_INIT\_TRACING を呼び出すと、ログ記録が有効になりません。

-   [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)が失敗した場合、呼び出しは NULL ハンドルを返します。 その場合は、 **WppRecorderLogCreate**の戻り値を無視し、RECODER\_ログハンドルを使用して、WPP メッセージを出力することができます。

-   [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))によって返されたハンドルは削除しないでください。 既定のログを無効にするには、レコーダーの**Createdefaultlog**メンバー [ **\_CONFIGURE\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)を FALSE に設定してから、 [**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)を呼び出します。

-   既定のログハンドルを渡すことで[**WppRecorderLogSetIdentifier**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogsetidentifier)を呼び出さないでください。 この操作は許可されていません。

-   IFR バッファーは、非ページプールから割り当てられます。 これらの割り当ての累積効果は、特に小さいフットプリントデバイスでは、パフォーマンスに大きな問題が生じる可能性があります。 [**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)のバッファーサイズを小さくするように要求します。 また、ログ記録機能が不要な場合は、既定のログを無効にしてください。

-   ログバッファーのサイズを表示するには、 [ **! wdfkd. wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)コマンドを使用します。 [Rcdrkd 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)を使用している場合は、 [ **! rcdrkd. rcdrloglist**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-rcdrkd-rcdrloglist)を使用してサイズを表示できます。

## <a name="span-idumdf_and_kmdf_differencesspanspan-idumdf_and_kmdf_differencesspanspan-idumdf_and_kmdf_differencesspanumdf-and-kmdf-differences"></a><span id="UMDF_and_KMDF_differences"></span><span id="umdf_and_kmdf_differences"></span><span id="UMDF_AND_KMDF_DIFFERENCES"></span>UMDF と KMDF の相違点


-   カスタムバッファーを作成できるのは、カーネルモードのドライバーだけです。 この機能は、ユーザーモードドライバーには適用されません。
-   [Rcdrkd 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)を使用して、ユーザーモードドライバーからトレースログを表示することはできません。 [Wdfkd 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)を使用する必要があります。









