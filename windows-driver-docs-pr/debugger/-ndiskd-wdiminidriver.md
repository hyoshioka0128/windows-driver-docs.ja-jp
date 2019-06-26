---
title: ndiskd.wdiminidriver
description: Ndiskd.wdiminidriver 拡張機能には、1 つまたは複数の CMiniportDriver 構造に関する情報が表示されます。
ms.assetid: C7022CD7-6F3A-485B-8686-A686A5305DA5
keywords:
- デバッグ ndiskd.wdiminidriver Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.wdiminidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f4af011cb79092c1483f34cda8c0ad4c100ce10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363094"
---
# <a name="ndiskdwdiminidriver"></a>!ndiskd.wdiminidriver


**! Ndiskd.wdiminidriver**拡張機能は、1 つまたは複数の CMiniportDriver 構造に関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd CMiniportDriver 構造体のすべての一覧が表示されます。

WDI ミニポート ドライバーの詳細については、次を参照してください。、 [WDI ミニポート ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)します。

WDI ミニポート ドライバー リファレンスの詳細については、次を参照してください。 [WDI ミニポート ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

```console
!ndiskd.wdiminidriver [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
CMiniportDriver オブジェクトのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
ミニポート ドライバーに関する基本情報が表示されます。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
このドライバーのミニポート ハンドラーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.wdiminidriver** CMiniportDriver のすべてのオブジェクトの一覧を表示するパラメーターなしで拡張機能。 次の例では、1 つだけの CMiniportDriver オブジェクトがあります。 その WdiMiniDriver のハンドルは、ffffc804b8ce7c40 です。

```console
1: kd> !ndiskd.wdiminidriver
    WdiMiniDriver      Name                                                     
    ffffc804b8ce7c40 - WDI MiniDriver
```

WdiMiniDriver のハンドルをクリックするか、入力、 **! ndiskd.wdiminidriver-処理**WDI ミニポート ドライバーの詳細を表示するコマンド。

```console
1: kd> !ndiskd.wdiminidriver ffffc804b8ce7c40


WDI MINIPORT DRIVER

    Object             ffffc804b8ce7c40
    DRIVER_OBJECT      ffffc804b90a4ac0

    Ndis API version   v6.50
    NDIS driver        ffffc804af2e3710 - mrvlpcie8897
    Driver version     v1.0
    WDI API version    v1.0.1


    Handlers
```

WDI ミニポート ドライバーの詳細情報の下部にある「ハンドラー」リンクをクリックするようになりましたまたはハンドルを使用して入力することができます、 **! ndiskd.wdiminidriver-処理 - ハンドラー**コマンドは、すべてこの WDI ミニポート ドライバーのハンドラーの一覧を表示します。

```console
1: kd> !ndiskd.wdiminidriver ffffc804b8ce7c40 -handlers


HANDLERS

    Miniport Handler                       Function pointer   Symbol (if available)
    InitializeHandlerEx                    [None]
    SetOptionsHandler                      fffff80965e8cae0   mrvlpcie8897!wlan_cmd_queue_deinit
    UnloadHandler                          fffff80965e71a08   mrvlpcie8897!MPUnload
    HaltHandlerEx                          [None]
    ShutdownHandlerEx                      fffff80965e71974   mrvlpcie8897!MPShutdown

    CheckForHangHandlerEx                  [None]
    ResetHandlerEx                         [None]

    PauseHandler                           [None]
    RestartHandler                         [None]

    OidRequestHandler                      [None]
    SendNetBufferListsHandler              [None]
    ReturnNetBufferListsHandler            [None]
    CancelSendHandler                      [None]
    CancelOidRequestHandler                [None]
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80965e71868   mrvlpcie8897!MPPnPEventNotify

    AllocateAdapterHandler                 fffff80965e713ec   mrvlpcie8897!MPAllocateTalAdapter
    FreeAdapterHandler                     fffff80965e717e8   mrvlpcie8897!MPFreeTalAdapter
    OpenAdapterHandler                     fffff80965e719b8   mrvlpcie8897!MPTaskOpenHandler
    CloseAdapterHandler                    fffff80965e719ac   mrvlpcie8897!MPTaskCloseHandler
    StartOperationHandler                  [None]
    StopOperationHandler                   [None]
    PostPauseHandler                       [None]
    PostRestartHandler                     [None]
    HangDiagnoseHandler                    fffff80965e715d8   mrvlpcie8897!MPDiagnosticHandler
    TalTxRxInitializeHandler               fffff80965e752d4   mrvlpcie8897!TalDataPathInitialize
    TalTxRxDeinitializeHandler             fffff80965e7527c   mrvlpcie8897!TalDataPathDeinitialize

    OpenAdapterCompleteHandler             fffff80965ffab50   wdiwifi!WDIOpenAdapterCompleteHandler
    CloseAdapterCompleteHandler            fffff80965fface0   wdiwifi!WDICloseAdapterCompleteHandler
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[WDI ミニポート ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI ミニポート ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






