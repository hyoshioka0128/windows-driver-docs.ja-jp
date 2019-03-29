---
title: ndiskd.filter
description: Ndiskd.filter 拡張機能では、NDIS 軽量フィルター (LWF) に関する情報が表示されます。 パラメーターなしでこの拡張機能を実行する場合 ndiskd すべて LWFs の一覧が表示されます。
ms.assetid: 4cf0f8bc-a15a-49db-b7db-13d60fd0c767
keywords:
- デバッグ ndiskd.filter Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 294b53f8dc106c61712fc123b4b535a988d5ffab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579691"
---
# <a name="ndiskdfilter"></a>!ndiskd.filter


**! Ndiskd.filter**拡張機能は、NDIS 軽量フィルター (LWF) に関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd すべて LWFs の一覧が表示されます。

```console
!ndiskd.filter [-handle <x>] [-findname <any>] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 軽量フィルターのハンドル。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
LWFs を名のプレフィックスでフィルター処理します。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
この LWF のフィルターのハンドラーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

入力、 **! ndiskd.filter**コマンドとパラメーターのないすべてのフィルターの一覧を取得します。 この例では、ffff8083e14e8460 ハンドルを探します。 このハンドルは、フィルター自体とその関連付けられたフィルターの下に入れ子になっている*ドライバー*、QoS パケット スケジューラ。

```console
3: kd> !ndiskd.filter
ffff8083e1a7fd90 - QoS Packet Scheduler
  Filter ffff8083e14e8460, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e1a96b80 - Virtual WiFi Filter Driver
ffff8083e19c4b70 - WFP vSwitch Layers LightWeight Filter
ffff8083e19a6ad0 - WFP Native MAC Layer LightWeight Filter
  Filter ffff8083e43df8f0, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e19a6d70 - WFP 802.3 MAC Layer LightWeight Filter
  Filter ffff8083e0d89c70, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
```

このフィルターのハンドルを使用したことがわかりますがなどについてより詳細な情報の状態より高いフィルター ハンドル、およびフィルターの下部のハンドル。

```console
3: kd> !ndiskd.filter ffff8083e14e8460


FILTER

    Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000

    Ndis handle        ffff8083e14e8460
    Filter driver      ffff8083e1a7fd90 - QoS Packet Scheduler
    Module context     ffff8083e26953e0
    Miniport           ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
    Network interface  ffff8083e200f010

    State              Running
    Datapath           Send only
    References         1
    Flags              RUNNING
    More flags         OID_TOP

    Higher filter      ffff8083e0d89c70 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    Lower filter       ffff8083e43df8f0 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000

    Driver handlers
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






