---
title: usb3kd.xhci_commandring
description: Usb3kd.xhci_commandring 拡張機能では、USB 3.0 ホスト コント ローラーに関連付けられているコマンドのリングのデータ構造に関する情報が表示されます。
ms.assetid: 3099F3F1-B881-4BBD-90F5-59DC2DFECF3B
keywords:
- デバッグ usb3kd.xhci_commandring Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_commandring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16afbd844b7a29c2b15db887ca83a44110c92411
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572533"
---
# <a name="usb3kdxhcicommandring"></a>! usb3kd.xhci\_commandring


[ **! Usb3kd.xhci\_commandring** ](-usb3kd-device-info.md)拡張機能は、USB 3.0 ホスト コント ローラーに関連付けられているコマンドのリング データ構造に関する情報を表示します。

```dbgcmd
!usb3kd.xhci_commandring DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能の AAddress します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

出力、 **! xhci\_commandring**コマンドは、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づきます。 USB 3.0 ホスト コント ローラーのドライバーと USB スタック内の他のドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)します。

コマンドのリングは、ホスト コント ローラーにコマンドを渡すために、USB 3.0 ホスト コント ローラー ドライバーによって使用データ構造です。

<a name="examples"></a>使用例
--------

デバイス拡張機能のアドレスを取得する出力の確認、 [ **! xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)コマンド。 次の例では、デバイスの拡張機能のアドレスは、0xfffffa800536e2d0 です。

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
    ...
```

デバイスの拡張機能のアドレスを渡すことができますので、 **! xhci\_commandring**コマンド。

```dbgcmd
3: kd> !xhci_commandring 0xfffffa800536e2d0

## Dumping dt _COMMAND_DATA 0xfffffa8005362f70 !rcdrlogdump USBXHCI -a 0xfffffa8005a8f010
-------------------------------------------------------------------------------------
Stop: OFF Abort: OFF Running: ON
CommandRingBufferData: VA 0xfffffa8005aeb200 LA 0x1168eb200 !wdfcommonbuffer 0x57ffa65d988 Size 512
DequeueIndex: 24 EnqueueIndex: 24 CycleState: 0

    Command Ring TRBs:
        [  0] Unknown TRB Type 49 0xfffffa8005aeb200

        [  1] ENABLE_SLOT                 0xfffffa8005aeb210 CycleBit 1
        [  2] ADDRESS_DEVICE              0xfffffa8005aeb220 CycleBit 1 SlotId  1 BlockSetAddressRequest 1
        ...

    PendingList:
        Empty List

    WaitingList:
        Empty List
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






