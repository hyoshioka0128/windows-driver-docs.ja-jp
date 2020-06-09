---
title: usbkd. usbportmdportlog
description: Usbkd. usbportmdportlog コマンドを実行すると、USBKD デバッグログが、バグチェック0xFE の結果として生成されたクラッシュダンプに存在する場合に表示されます。
ms.assetid: C0E32BDE-8186-4477-AB57-530B0AF6F27F
keywords:
- usbkd. usbportmdportlog Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmdportlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbc3e3e9610c15a62a73a0384563ca7088a470c0
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534681"
---
# <a name="usbkdusbportmdportlog"></a>!usbkd.usbportmdportlog


[**Bug Check 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプに存在する場合は、 **! usbkd. usbportmdportlog**コマンドによって usbkd デバッグログが表示されます。

```dbgcmd
!usbkd.usbportmdportlog
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

<a name="examples"></a>例
--------

次に、 **! usbportmdportlog**の出力の一部の例を示します。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.usbportmdportlog
Minidump USBPORT DEBUG_LOG buffer size 32768, entries 1024, index 400
*LOG: 0000000113be9600  LOGSTART: 0000000113be6400 *LOGEND: 0000000113bee3e0 # 1024 
[ 000] 0000000113be9600 Bfe2 ffffe0001416802c ffffe000020a44f0 ffffe0001416801c 
[ 001] 0000000113be9620 Bfe0 0000000000000000 ffffe000039f4720 ffffe00000b76cb0 
[ 002] 0000000113be9640 epr+ ffffe000043ee010 ffffe000008f5b80 ffffe00002820a0c 
[ 003] 0000000113be9660 alTR ffffe00002820a0c ffffe000039f4720 ffffe00000b76cb0 
//
// USBPORT_Core_AllocTransferEx()
// transfer:                ffffe00002820a0c
// Urb:                     ffffe000039f4720
// Irp:                     ffffe00000b76cb0

[ 004] 0000000113be9680 TRcs 0000000000000060 0000000000000468 0000000000000001 
[ 005] 0000000113be96a0 urbi ffffe0001422c4cc 0000000000000012 000000000000000b 
[ 006] 0000000113be96c0 dURB ffffe000039f4720 ffffe00000b76cb0 000000000000000b 
//
// USBPORT_ProcessURB() - Device Handle valid and has been referenced
// Urb:                     ffffe000039f4720
// Irp:                     ffffe00000b76cb0
// function:                URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE

[ 007] 0000000113be96e0 vld> ffffe0001421ddd0 0000000000000004 ffffe000039f4720 
//
// USBPORT_NeoValidDeviceHandle()
// DeviceHandle:            ffffe0001421ddd0
// ReferenceObj:            ffffe000039f4720

[ 008] 0000000113be9700 devH ffffe0001421ddd0 ffffe000039f4720 0000000000000000 
[ 009] 0000000113be9720 pURB ffffe000039f4720 ffffe00000b76cb0 000000000000000b 
//
// USBPORT_ProcessURB()
// Urb:                     ffffe000039f4720
// Irp:                     ffffe00000b76cb0
// function:                URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE

[ 010] 0000000113be9740 PURB ffffe000039f4720 ffffe000020a44f0 000000000000000b 
//
// USBPORT_ProcessURB() - Exit STATUS_PENDING
// Urb:                     ffffe000039f4720
// Irp:                     ffffe000020a44f0
// function:                URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE

[ 011] 0000000113be9760 Urb< 0000000000000103 000000000000000b 0000000000000000 
[ 012] 0000000113be9780 xSt0 ffffe000012bbf18 0000000000000006 0000000000000001 
[ 013] 0000000113be97a0 xnd8 ffffe000012bbf18 ffffe000012bb050 0000000000000000 
[ 014] 0000000113be97c0 xnd0 ffffe000012bbf18 ffffe000012bb050 0000000000000000 
//
// USBPORT_Xdpc_End()

[ 015] 0000000113be97e0 mapF 0000000000000000 0000000000000000 0000000000000000 
[ 016] 0000000113be9800 map5 0000000000000000 0000000000000000 0000000000000000 
[ 017] 0000000113be9820 DMAx 0000000000000000 0000000000000000 0000000000000000 
[ 018] 0000000113be9840 subx 0000000000000000 0000000000000000 ffffe0001416801c 
[ 019] 0000000113be9860 tmoZ 0000000000000000 ffffe0001416801c ffffe000141680a4 
...
...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






