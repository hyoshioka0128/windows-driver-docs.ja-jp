---
title: usb3kd.port_info
description: Usb3kd.port_info コマンドでは、USB 3.0 ツリーの中に USB ポートに関する情報が表示されます。
ms.assetid: 78233FE5-981E-42C4-A100-198CAAA840A0
keywords:
- デバッグ usb3kd.port_info Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.port_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 015237962c3954dc7bf8fa1bff283425fe838398
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338721"
---
# <a name="usb3kdportinfo"></a>!usb3kd.port\_info


[ **! Usb3kd.port\_情報**](-usb3kd-device-info.md)コマンドでの USB ポートに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。

```dbgcmd
!usb3kd.port_info PortContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PortContext______"></span><span id="_______portcontext______"></span><span id="_______PORTCONTEXT______"></span> *PortContext*   
アドレスを\_ポート\_CONTEXT 構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>例
--------

出力ポートのコンテキストのアドレスを取得するには、確認、 [ **! usb\_ツリー** ](-usb3kd-usb-tree.md)コマンド。 次の例では、ポートのコンテキストのアドレスは、0xfffffa8005abe0c0 です。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        ...
        !port_info 0xfffffa8005abe0c0 !device_info 0xfffffa8005abd0c0 Desc: ... USB Flash Drive Speed: Super
```

ポートのコンテキストのアドレスを渡すことができますので、 **! ポート\_情報**コマンド。

```dbgcmd
3: kd> !port_info 0xfffffa8005abe0c0

## Dumping Port Context 0xfffffa8005abe0c0
---------------------------------------
dt USBHUB3!_PORT_CONTEXT 0xfffffa8005abe0c0
!hub_info 0xfffffa8005ad92d0 (dt _HUB_FDO_CONTEXT 0xfffffa8005ad92d0)
!device_info 0xfffffa8005abd0c0 (dt _DEVICE_CONTEXT 0xfffffa8005abd0c0)
!rcdrlogdump usbhub3 -a 0xfffffa8005abf6b0

PortNumber: 2
Last Port Status(3.0): Connected Enabled Powered
Last Port Change: <none>

CurrentPortEvent: PsmEventPortConnectChange
Current Port(3.0) State: ConnectedEnabled.WaitingForPortChangeEvent

Port(3.0) State History: <Event> NewState (<Operation>(),..) :

    [34] <Push> WaitingForPortChangeEvent 
    ...
Port Event History:
    [ 8] TransferSuccess
    ...  
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






