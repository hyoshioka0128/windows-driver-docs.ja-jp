---
title: ndiskd wdiminidriver
description: Wdiminidriver 拡張機能には、1つ以上の CMiniportDriver 構造に関する情報が表示されます。
ms.assetid: C7022CD7-6F3A-485B-8686-A686A5305DA5
keywords:
- wdiminidriver Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.wdiminidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 050836ff1ff43cf0bebcd10a40d2a734dafca369
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837647"
---
# <a name="ndiskdwdiminidriver"></a>!ndiskd.wdiminidriver


**! Ndiskd**拡張機能には、1つ以上の CMiniportDriver 構造に関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべての CMiniportDriver 構造体の一覧が表示されます。

WDI ミニポートドライバーの詳細については、「 [WDI ミニポートドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)」を参照してください。

WDI ミニポートドライバーリファレンスの詳細については、「 [WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

```console
!ndiskd.wdiminidriver [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
CMiniportDriver オブジェクトのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
ミニポートドライバーに関する基本的な情報を表示します。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
このドライバーのミニポートハンドラーを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

すべての CMiniportDriver オブジェクトの一覧を表示するには、パラメーターを使用せずに **! ndiskd wdiminidriver**拡張機能を実行します。 次の例では、CMiniportDriver オブジェクトが1つだけ存在します。 WdiMiniDriver のハンドルは ffffc804b8ce7c40 です。

```console
1: kd> !ndiskd.wdiminidriver
    WdiMiniDriver      Name                                                     
    ffffc804b8ce7c40 - WDI MiniDriver
```

WdiMiniDriver のハンドルをクリックするか、 **! ndiskd WdiMiniDriver**コマンドを入力して、この WDI ミニポートドライバーの詳細を確認します。

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

これで、WDI ミニポートドライバーの詳細の下部にある [ハンドラー] リンクをクリックしたり、ハンドルを使用して **! ndiskd**コマンドを入力して、この WDI ミニポートドライバーのすべてのハンドラーの一覧を表示したりすることができます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[WDI ミニポートドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






