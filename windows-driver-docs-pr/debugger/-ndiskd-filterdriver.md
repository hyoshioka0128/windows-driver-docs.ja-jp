---
title: ndiskd.filterdriver
description: Ndiskd.filterdriver 拡張機能では、NDIS フィルター ドライバーに関する情報が表示されます。 パラメーターなしでこの拡張機能を実行すると、ndiskd により、すべてのフィルター ドライバーの一覧が表示されます。
ms.assetid: 9FE3E885-98BC-4FCC-9E1C-DBECD070F92A
keywords:
- デバッグ ndiskd.filterdriver Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filterdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 91a427bddfa9b2801853b341e020679670fb8cac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549173"
---
# <a name="ndiskdfilterdriver"></a>! ndiskd.filterdriver


**! Ndiskd.filterdriver**拡張機能は、NDIS フィルター ドライバーに関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd すべてのフィルター ドライバーの一覧が表示されます。

```console
!ndiskd.filterdriver [-handle <x>] [-filters] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS フィルター ドライバーのハンドル。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span> *-フィルター*   
このドライバーのフィルターのインスタンスが表示されます。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
このドライバーのフィルターのハンドラーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行 **! ndiskd.filterdriver**パラメーターのないシステムのすべてのフィルター ドライバーの一覧を表示します。 次の例では、そのハンドルは ffffbc064cc83be0 仮想、WiFi フィルター ドライバーを探します。

```console
0: kd> !ndiskd.filterdriver
    ffffbc064ccd4900 - QoS Packet Scheduler
    ffffbc064cc83be0 - Virtual WiFi Filter Driver
    ffffbc064cb91a10 - WFP vSwitch Layers LightWeight Filter
    ffffbc064cb8fd70 - WFP Native MAC Layer LightWeight Filter
    ffffbc064cb59b00 - WFP 802.3 MAC Layer LightWeight Filter
```

フィルター ドライバーをクリックして処理前の例から、または入力に使用することによって、 **! ndiskd.filterdriver-処理**コマンド ウィンドウでコマンドを表示するフィルター ドライバーの詳細情報を取得できます。 この場合、たとえばはありませんフィルター ドライバーのフィルター モジュールです。

```console
0: kd> !ndiskd.filterdriver ffffbc064cc83be0


FILTER DRIVER

    Virtual WiFi Filter Driver

    Ndis handle        ffffbc064cc83be0
    Driver context     ffffbc064cc8e9d0
    Ndis API version   v6.50
    Driver version     v1.0
    Driver object      ffffbc064cc8e9d0
    Driver image       vwififlt.sys

    Bind flags         Optional, Modifying
    Class              [Zero-length string]
    References         1


FILTER MODULES

    Filter module                                                               
    [No filter modules were found]


HANDLERS

    Filter handler                         Function pointer   Symbol (if available)
    SetOptionsHandler                      [None]
    SetFilterModuleOptionsHandler          [None]
    AttachHandler                          fffff80787d83b60  bp
    DetachHandler                          fffff80787d84800  bp
    RestartHandler                         fffff80787d86e20  bp
    PauseHandler                           fffff80787d863e0  bp
    SendNetBufferListsHandler              fffff80787d814d0  bp
    SendNetBufferListsCompleteHandler      fffff80787d81940  bp
    CancelSendNetBufferListsHandler        fffff80787d842f0  bp
    ReceiveNetBufferListsHandler           fffff80787d817e0  bp
    ReturnNetBufferListsHandler            fffff80787d81a80  bp
    OidRequestHandler                      fffff80787d85ae0  bp
    OidRequestCompleteHandler              fffff80787d85fd0  bp
    DirectOidRequestHandler                fffff80787d84af0  bp
    DirectOidRequestCompleteHandler        fffff80787d84e80  bp
    CancelDirectOidRequestHandler          fffff80787d841d0  bp
    DevicePnPEventNotifyHandler            fffff80787d849e0  bp
    NetPnPEventHandler                     fffff80787d85a40  bp
    StatusHandler                          fffff80787d877c0  bp
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






