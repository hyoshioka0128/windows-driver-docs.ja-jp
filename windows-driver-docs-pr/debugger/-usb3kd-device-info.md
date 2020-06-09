---
title: device_info usb3kd
description: Device_info usb3kd コマンドは、usb 3.0 ツリーの USB デバイスに関する情報を表示します。
ms.assetid: BD6D1562-2606-42C1-9EE6-D38D93D685DE
keywords:
- usb3kd Windows デバッグの device_info
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82bb10b26d035fdafea0d57e8cd6832dd54eb090
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534903"
---
# <a name="usb3kddevice_info"></a>! usb3kd. デバイス \_ 情報


**! Usb3kd \_ **コマンドを実行すると、usb デバイスに関する情報が[usb 3.0 ツリー](usb-3-extensions.md#usb-3-tree)に表示されます。

```dbgcmd
!usb3kd.device_info DeviceContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceContext______"></span><span id="_______devicecontext______"></span><span id="_______DEVICECONTEXT______"></span>*Devicecontext*   
\_デバイスを表すデバイス \_ コンテキスト構造のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! デバイス \_ 情報**と[**! ucx \_ デバイス**](-usb3kd-ucx-device.md)の両方にデバイスに関する情報が表示されますが、表示される情報は異なります。 **デバイス \_ 情報**の出力は、usb 3.0 hub ドライバーの観点から見たものであり、 **! ucx \_ デバイス**の出力は、usb ホストコントローラー拡張機能ドライバーの観点からのものです。 たとえば、 **! デバイス \_ 情報**出力には、構成記述子とインターフェイス記述子に関する情報が含まれています。また、 **! ucx \_ デバイス**出力には、エンドポイントに関する情報が含まれています。

<a name="examples"></a>例
--------

デバイスコンテキスト構造のアドレスを取得するには、 [**! usb \_ ツリー**](-usb3kd-usb-tree.md)コマンドの出力を参照します。 次の例では、デバイスコンテキスト構造のアドレスは0xfffffa8005abd0c0 です。

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

これで、デバイスコンテキストのアドレスを **! device \_ info**コマンドに渡すことができるようになりました。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! usb3kd \_ \_ pdo からのデバイス \_ 情報**](-usb3kd-device-info-from-pdo.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






