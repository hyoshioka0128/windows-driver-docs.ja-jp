---
title: ndiskd フィルター
description: Ndiskd フィルター拡張機能には、NDIS ライトウェイトフィルター (LWF) に関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、ndiskd はすべての LWFs の一覧を表示します。
ms.assetid: 4cf0f8bc-a15a-49db-b7db-13d60fd0c767
keywords:
- ndiskd Windows デバッグのフィルター処理
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 946a669c7eedef831a5c8f0e33d390d634c4abc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837596"
---
# <a name="ndiskdfilter"></a>!ndiskd.filter


**! Ndiskd フィルター**拡張機能には、NDIS ライトウェイトフィルター (lwf) に関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべての LWFs の一覧が表示されます。

```console
!ndiskd.filter [-handle <x>] [-findname <any>] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
NDIS ライトウェイトフィルターのハンドル。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
名前プレフィックスで LWFs をフィルター処理します。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
この LWF のフィルターハンドラーを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

すべてのフィルターの一覧を取得するには、パラメーターを指定せずに **! ndiskd filter**コマンドを入力します。 この例では、ffff8083e14e8460 ハンドルを探します。 このハンドルはフィルター自体を対象とし、関連付けられているフィルター*ドライバー*(QoS パケットスケジューラ) の下に入れ子になっていることに注意してください。

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

このフィルターハンドルを使用すると、it の状態、上位のフィルターハンドル、下位のフィルターハンドルなど、詳細な情報が表示されるようになりました。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

 

 






