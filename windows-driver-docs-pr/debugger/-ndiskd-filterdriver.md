---
title: ndiskd filterdriver
description: Ndiskd filterdriver 拡張機能には、NDIS フィルタードライバーに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべてのフィルタードライバーの一覧が表示されます。
ms.assetid: 9FE3E885-98BC-4FCC-9E1C-DBECD070F92A
keywords:
- ndiskd filterdriver Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filterdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0588f6c6eb7f17bfd461c3573b4fa125d08be79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826664"
---
# <a name="ndiskdfilterdriver"></a>!ndiskd.filterdriver


**! Ndiskd filterdriver**拡張機能には、NDIS フィルタードライバーに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべてのフィルタードライバーの一覧が表示されます。

```console
!ndiskd.filterdriver [-handle <x>] [-filters] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
NDIS フィルタードライバーのハンドル。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span> *-フィルター*   
このドライバーのフィルターのインスタンスを表示します。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
このドライバーのフィルターハンドラーを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

システム上のすべてのフィルタードライバーの一覧を表示するには、パラメーターを付けずに **! ndiskd**を実行します。 次の例では、仮想 WiFi フィルタードライバーのハンドルが ffffbc064cc83be0 であることを確認します。

```console
0: kd> !ndiskd.filterdriver
    ffffbc064ccd4900 - QoS Packet Scheduler
    ffffbc064cc83be0 - Virtual WiFi Filter Driver
    ffffbc064cb91a10 - WFP vSwitch Layers LightWeight Filter
    ffffbc064cb8fd70 - WFP Native MAC Layer LightWeight Filter
    ffffbc064cb59b00 - WFP 802.3 MAC Layer LightWeight Filter
```

前の例のフィルタードライバーハンドルをクリックするか、またはそれを使用してコマンドウィンドウに **! ndiskd. filterdriver-handle**コマンドを入力すると、そのフィルタードライバーに関する詳細情報が表示されます。 この場合、たとえば、このフィルタードライバーにはフィルターモジュールがありません。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






