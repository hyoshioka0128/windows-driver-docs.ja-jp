---
title: devext
description: Devext 拡張機能では、バスのさまざまなデバイスのバスに固有のデバイスの拡張機能情報が表示されます。
ms.assetid: b4d4f595-9b0b-40e2-8790-2c913a50c8fe
keywords:
- usbhub の拡張機能 (廃止)
- hidfdo の拡張機能 (廃止)
- hidpdo の拡張機能 (廃止)
- デバイスの拡張機能
- バス
- Windows デバッグ devext
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81d31c09168df2ea28d43674313cfc2644cfcb52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334591"
---
# <a name="devext"></a>!devext


**! Devext**拡張機能のバスさまざまなデバイス用のバスに固有のデバイス拡張機能の情報を表示します。

```dbgcmd
!devext Address TypeCode
```

## <a name="span-idddkdevextdbgspanspan-idddkdevextdbgspanparameters"></a><span id="ddk__devext_dbg"></span><span id="DDK__DEVEXT_DBG"></span>パラメーター

###  <a name="address"></a>*Address*   
表示するデバイスの拡張機能の 16 進数のアドレスを指定します。

#### <a name="typecode"></a>*TypeCode*   
表示するデバイスの拡張機能を所有するオブジェクトの種類を指定します。 種類のコードは区別されません。 有効な種類のコードは次のとおりです。

|TypeCode|オブジェクト|
|--- |--- |
|ISAPNP|ISA PnP デバイスの拡張機能|
|PCMCIA|PCMCIA デバイス拡張機能|
|HID|HID デバイス拡張機能|
 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 デバイスの拡張機能の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

**! Usbhub**、 **! hidfdo**、および **! hidpdo**拡張機能が廃止されています。 以外にそれらの機能が統合されました **! devext**します。

これらのオブジェクトの種類ではサポートされなくなったため **! devext**を使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)デバッガー コマンド。

ISA PnP デバイスの拡張機能の例を次に示します。

```dbgcmd
kd> !devext e0000165fff32190 ISAPNP
ISA PnP FDO @ 0x00000000, DevExt @ 0xe0000165fff32190, Bus # 196639
Flags (0x854e2530)  DF_ACTIVATED, DF_QUERY_STOPPED, 
                    DF_STOPPED, DF_RESTARTED_NOMOVE, 
                    DF_BUS
                    Unknown flags 0x054e2000

NumberCSNs           - -536870912
ReadDataPort         - 0x0000000d (mapped)
AddressPort          - 0x00000000 (not mapped)
CommandPort          - 0x00000000 (not mapped)
DeviceList           - 0xe000000085007b50
CardList             - 0x00000000
PhysicalBusDevice    - 0x00000000
AttachedDevice       - 0x00000000
SystemPowerState     - Unspecified
DevicePowerState     - Unspecified
```

PCI デバイスの例を次に示します。

```dbgcmd
kd> !devext e0000000858c31b0 PCI
PDO Extension, Bus 0x0, Device 0, Function 0.
  DevObj 0xe0000000858c3060 PCI Parent Bus FDO DevExt 0xe0000000858c4960
  Device State = PciNotStarted
  Vendor ID 8086 (INTEL)  Device ID 123D
  Class Base/Sub 08/00  (Base System Device/Interrupt Controller)
  Programming Interface: 20, Revision: 01, IntPin: 00, Line Raw/Adj 00/00
  Enables ((cmd & 7) = 106): BM   Capabilities Pointer = <none>
  CurrentState:          System Working,  Device D0
  WakeLevel:             System Unspecified,  Device Unspecified
  Requirements: <none>
```

 

 





