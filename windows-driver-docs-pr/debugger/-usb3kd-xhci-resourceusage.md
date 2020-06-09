---
title: xhci_resourceusage usb3kd
description: Xhci_resourceusage usb3kd 拡張機能は、USB 3.0 ホストコントローラーによって使用されているリソースを表示します。
ms.assetid: 6AAB64D6-3CDA-4BA2-BBA8-F2F5AD1DBB6F
keywords:
- usb3kd Windows デバッグの xhci_resourceusage
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_resourceusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d4a096ee259ceec28a3d72babc726782a91543f
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534112"
---
# <a name="usb3kdxhci_resourceusage"></a>! usb3kd. xhci \_ resourceusage


[**! Usb3kd xhci \_ resourceusage**](-usb3kd-device-info.md)拡張機能によって、USB 3.0 ホストコントローラーによって使用されているリソースが表示されます。

```dbgcmd
!usb3kd.xhci_resourceusage DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*Deviceextension*   
ホストコントローラーの機能デバイスオブジェクト (FDO) のデバイス拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

出力の **! xhci \_ resourceusage**コマンドは、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB スタック内のその他のドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://docs.microsoft.com//windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

<a name="examples"></a>例
--------

デバイス拡張機能のアドレスを取得するには、 [**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)コマンドの出力を確認します。 次の例では、デバイス拡張機能のアドレスは0xfffffa800536e2d0 です。

```dbgcmd
3: kd> !xhci_dumpall

## Dumping all the XHCI controllers - DrvObj 0xfffffa80053072f0
------------------------------------------------------------
1)  ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    !xhci_resourceusage 0xfffffa800536e2d0
    ...
```

これで、デバイス拡張機能のアドレスを **! xhci \_ resourceusage**コマンドに渡すことができます。

```dbgcmd
 3: kd> !xhci_resourceusage 0xfffffa800536e2d0

## Dumping CommonBuffer Resources
------------------------------
    dt USBXHCI!_COMMON_BUFFER_DATA 0xfffffa80059a5920
    DmaEnabler:!wdfdmaenabler 0x57ffa65a9c8

    CommonBuffers Large: Total 9 Available 2 Used 7 TotalBytes 36864
        [ 1] dt _TRACKING_DATA 0xfffffa80059a6768 VA 0xfffffa8005370000 LA 0x117170000 ...
        [ 2] dt _TRACKING_DATA 0xfffffa80059a4768 VA 0xfffffa8005373000 LA 0x117173000 ...
        ...
    CommonBuffers Small: Total 32 Available 8 Used 24 TotalBytes 16384
        [ 1] dt _TRACKING_DATA 0xfffffa80059a2798 VA 0xfffffa8005aeb000 LA 0x1168eb000 ...
        [ 2] dt _TRACKING_DATA 0xfffffa80059a27e8 VA 0xfffffa8005aeb200 LA 0x1168eb200 ...
        ...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






