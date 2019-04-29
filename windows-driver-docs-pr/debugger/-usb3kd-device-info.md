---
title: usb3kd.device_info
description: Usb3kd.device_info コマンドでは、USB 3.0 ツリーの中に USB デバイスに関する情報が表示されます。
ms.assetid: BD6D1562-2606-42C1-9EE6-D38D93D685DE
keywords:
- デバッグ usb3kd.device_info Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86f6872f33878d36433f939c75841de65a9fa4b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335665"
---
# <a name="usb3kddeviceinfo"></a>!usb3kd.device\_info


**! Usb3kd.device\_情報**コマンドで USB デバイスに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。

```dbgcmd
!usb3kd.device_info DeviceContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceContext______"></span><span id="_______devicecontext______"></span><span id="_______DEVICECONTEXT______"></span> *DeviceContext*   
アドレス、\_デバイス\_デバイスを表すコンテキスト構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

**! デバイス\_情報**と[ **! ucx\_デバイス**](-usb3kd-ucx-device.md)デバイスに関する情報の両方が表示が表示される情報は異なります。 出力 **! デバイス\_情報**は USB 3.0 ハブのドライバーの point of view およびの出力から **! ucx\_デバイス**USB ホスト コント ローラー拡張機能の観点からは、ドライバー。 たとえば、 **! デバイス\_情報**出力には、構成と記述子にはインターフェイスに関する情報が含まれていますと **! ucx\_デバイス**出力に関する情報が含まれます。エンドポイント。

<a name="examples"></a>例
--------

デバイス コンテキストの構造体のアドレスを取得するには、出力を調べることで、 [ **! usb\_ツリー** ](-usb3kd-usb-tree.md)コマンド。 次の例では、デバイス コンテキストの構造体のアドレスは、0xfffffa8005abd0c0 です。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
    ...
## Enumerated Device List
----------------------
...

2) !device_info 0xfffffa8005abd0c0, !devstack fffffa80059c3800
    Current Device State: ConfiguredInD0
    Desc: ... USB Flash Drive
    ...
```

デバイス コンテキストのアドレスを渡すことができますので、 **! デバイス\_情報**コマンド。

```dbgcmd
3: kd> !device_info 0xfffffa8005abd0c0

## Dumping Device Information fffffa8005abd0c0
-------------------------------------------
dt USBHUB3!_DEVICE_CONTEXT 0xfffffa8005abd0c0
dt USBHUB3!_HUB_PDO_CONTEXT 0xfffffa8005b118d0
!idle_info 0xfffffa8005b11920 (dt USBHUB3!_ISM_CONTEXT 0xfffffa8005b11920)
Parent !hub_info 0xfffffa8005ad92d0 (dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0)
!port_info 0xfffffa8005abe0c0 (dt USBHUB3!_PORT_CONTEXT 0xfffffa8005abe0c0)
!ucx_device 0xfffffa8005992840 !xhci_deviceslots 0xfffffa80051d1940 1

LPMState: U1IsEnabledForUpStreamPort U2IsEnabledForUpStreamPort U1Timeout: 38, U2Timeout: 3
DeviceFlags: HasContainerId NoBOSContainerId Removable HasSerialNumber MsOsDescriptorNotSupported NoWakeUpSupport DeviceIsSuperSpeedCapable 
DeviceHackFlags: WillDisableOnSoftRemove SkipSetIsochDelay WillResetOnResumeS0 DisableOnSoftRemove 

Descriptors:
dt _USB_CONFIGURATION_DESCRIPTOR 0xfffffa80053f9250
dt _USB_INTERFACE_DESCRIPTOR 0xfffffa80053f9259
ProductId: ... Flash Drive
DeviceDescriptor: VID ... PID ... REV 0a00,  Class: (0)(0) BcdUsb: 0300

UcxRequest: !wdfrequest 0x57ffa662948, 
ControlRequest: !wdfrequest 0x57ffa667798, !irp 0xfffffa8005997650 !urb 0xfffffa8005abd1c0, NumberOfBytes 0
Device working at SuperSpeed
Current Device State: ConfiguredInD0

Device State History: <Event> NewState (<Operation>(),..) :

    [16] <Yes> ConfiguredInD0
    ...
Device Event History:
    [10] TransferSuccess
    ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! usb3kd.device\_情報\_から\_pdo**](-usb3kd-device-info-from-pdo.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






