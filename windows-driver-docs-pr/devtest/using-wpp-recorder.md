---
title: トレースログ用の inflight トレースレコーダー (IFR)
description: Inflight トレースレコーダー (IFR) を使用すると、カーネルモードドライバーなどのトレースプロバイダーは、トレースログを記録し、WPP ログメッセージをバッファーに格納することができます。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 625e23664a5ed6833965f383851f007d2af1b284
ms.sourcegitcommit: d6909a8de7c5a4f87c86a08c055c841115823358
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80406419"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>トレースログ用の inflight トレースレコーダー (IFR)


*Inflight トレースレコーダー (IFR)* は、カーネルモードドライバーや UMDF ドライバーなどのトレースプロバイダーが、最新のログメッセージが保存されるメモリ内の循環バッファーのセットを作成するためのトレース機能です。 ログメッセージは、デバッガーを使用して表示できます。

IFR は、 [WPP ソフトウェアトレース](wpp-software-tracing.md)の上に構築されています。 IFR over WPP の主な利点は、自動的にオンになっていて、トレースセッションを事前に開始する必要がないことです。

**適用対象:**

-   最小 OS: KMDF および WDM ドライバー開発者向けの Windows 8
-   最小 OS: Windows 10 for UMDF (2.15) ドライバー開発者

## <a name="how-to-enable-inflight-trace-recorder-in-visual-studio"></a>Visual Studio で Inflight トレースレコーダーを有効にする方法

まず、「 [Windows ドライバーへの WPP ソフトウェアトレースの追加](adding-wpp-software-tracing-to-a-windows-driver.md)」の手順に従います。

次に、プロジェクトのプロパティページの **構成プロパティ-> WPP トレース-> 関数とマクロの > オプション** の下にある ok をクリックして、 **ok**を選択します。

最後に、UMDF の場合にのみ、追加のステップが1つあります。 **> 関数とマクロオプション > プリプロセッサの定義**については、`WPP_MACRO_USE_KM_VERSION_FOR_UM=1`を追加します。


## <a name="how-to-enable-inflight-trace-recorder-from-the-command-line"></a>コマンドラインから Inflight トレースレコーダーを有効にする方法

.Vcxproj ファイルを手動で編集する場合は、次のエントリを設定します。

KMDF または WDM ドライバーの場合:

```xml
    <ClCompile Include=...>
        <WppEnabled>true</WppEnabled>
        <WppKernelMode>true</WppKernelMode>
        <WppRecorderEnabled>true</WppRecorderEnabled>
        ...
    </ClCompile>
```

UMDF ドライバーの場合:

```xml
    <ClCompile Include=...>
        <WppEnabled>true</WppEnabled>
        <WppRecorderEnabled>true</WppRecorderEnabled>
        <WppPreprocessorDefinitions>WPP_MACRO_USE_KM_VERSION_FOR_UM=1</WppPreprocessorDefinitions>
        ...
    </ClCompile>
```


## <a name="how-to-send-trace-messages-to-the-default-log"></a>トレースメッセージを既定のログに送信する方法

「 [Windows ドライバーへの WPP ソフトウェアトレースの追加](adding-wpp-software-tracing-to-a-windows-driver.md)」の手順に従います。  例 :

 - [*Driverentry*](../wdf/driverentry-for-kmdf-drivers.md)で、`WPP_INIT_TRACING(DriverObject, RegistryPath)`を呼び出します。
 - [*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)で、`WPP_CLEANUP(WdfDriverWdmGetDriverObject(Driver))`を呼び出します。

ドライバーは、必要に応じてトレース関数を自由に呼び出すことができるようになりました。 たとえば次のようになります。`TraceEvents(TRACE_LEVEL_ERROR, DBG_INIT, "WdfDriverCreate failed, %!STATUS!", ntStatus);`

詳細については、 [WPP_INIT_TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556193(v%3Dvs.85))と[WPP_CLEANUP](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))に関する情報を参照してください。

## <a name="how-to-send-trace-messages-to-a-custom-log"></a>トレースメッセージをカスタムログに送信する方法

これは、カーネルモードドライバー (KMDF または WDM) にのみ適用されます。

ほとんどのドライバーでは、1つの既定のログで十分です。 ただし、シナリオによっては、個別のエンティティに個別のログバッファーを用意すると便利です。

たとえば、バスドライバーを作成する場合、各子デバイスに独自のバッファーが必要になることがあります。 その後、デバッガーを使用して、特定の子デバイスのログのみをダンプできます。

カスタムログをセットアップするには、ドライバーに `<WppRecorder.h>`が含まれている必要があります。 その後、次の Api を呼び出します。

 - 複数のログバッファーを作成する[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)
 - **WPP_CLEANUP**を呼び出す前に[**WppRecorderLogDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogdelete)を実行してください。
 - [**WppRecorderLogSetIdentifier**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogsetidentifier)を使用して、特定のレコーダーログの文字列識別子を設定します (省略可能)
 - [**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)を使用して既定のログを無効にする (省略可能)

また、ドライバーは、ログハンドルを最初のパラメーターとして受け取る新しいトレースマクロも定義する必要があります。 例については、[トースターサンプルドライバー](https://github.com/microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured/trace.h)を参照してください。


## <a name="how-to-view-trace-messages-in-the-debugger"></a>デバッガーでトレースメッセージを表示する方法

KMDF および UMDF ドライバーの場合は、通常どおり[ **! wdfkd. wdflogdump**](../debugger/-wdfkd-wdflogdump.md)を使用します。 フレームワークの IFR ログとドライバーの IFR ログの両方が出力されます。

WDM ドライバーの場合は、 [ **! rcdrkd. rcdrloglist**](../debugger/-rcdrkd-rcdrloglist.md)と[ **! rcdrkd. rcdrlogdump**](../debugger/-rcdrkd-rcdrlogdump.md)を使用します。


## <a name="configure-inflight-trace-recorder-parameters"></a>Inflight トレースレコーダーのパラメーターを構成する

IFR は、ドライバーの[パラメーターキー](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-registry-keys-for-drivers)の下で構成できます。

次のレジストリ値を使用します。

**LogPages: REG_DWORD**

既定のログを格納するページ数に設定します。 既定値は1です。

**VerboseOn: REG_DWORD**

既定値の0を設定すると、IFR ではエラー、警告、および情報イベントがログに記録されます。 ログに詳細出力を追加するには、1に設定します。
