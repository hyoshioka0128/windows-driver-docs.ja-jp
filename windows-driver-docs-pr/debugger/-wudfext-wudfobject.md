---
title: wudfext.wudfobject
description: Wudfext.wudfobject 拡張機能では、WDF オブジェクトとその親と子のリレーションシップに関する情報が表示されます。
ms.assetid: cb9398fb-24f5-4692-9a08-543bf1317b19
keywords:
- デバッグ wudfext.wudfobject Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfobject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10c5d683983efa900cb14cc5e0ac4f813357c59c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351596"
---
# <a name="wudfextwudfobject"></a>!wudfext.wudfobject


**! Wudfext.wudfobject**拡張機能は、WDF オブジェクトとその親と子のリレーションシップに関する情報を表示します。

```dbgcmd
!wudfext.wudfobject pWDFObject Flags TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFObject______"></span><span id="_______pwdfobject______"></span><span id="_______PWDFOBJECT______"></span> *pWDFObject*   
に関する情報を表示、WDF インターフェイスのアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
オブジェクト階層のリレーションシップが表示される親と子を取得する手順を再帰的にします。

<span id="Bit_1__0x02_"></span><span id="bit_1__0x02_"></span><span id="BIT_1__0X02_"></span>ビット 1 (0x02)  
オブジェクトに関する概要情報のみが表示されます。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 ビット (0x80)  
手順をオブジェクト階層を再帰的にし、内部のフレームワークの詳細を表示します。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
(省略可能)。 インターフェイスの種類を指定します (たとえば、 **IWDFDevice**)。 場合の値を*TypeName*は省略すると、拡張機能は、値としてインターフェイスの型。 場合、アスタリスク (\*) として提供されている*TypeName*、場合*TypeName*は省略すると、拡張機能しようとすると、指定されたインターフェイスの種類を自動的に決定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

使用することができます **! wudfext.wudfobject**などの子オブジェクトを一覧表示する、 **IWDFDevice**オブジェクトで、通常、デバイスのキューが含まれます。

使用することも **! wudfext.wudfobject** (たとえば、かどうか、WDF オブジェクトは削除処理中)、WDF オブジェクトの状態を確認するか、WDF を決定する特定のデバイスに関連付けられている WDF オブジェクトを検索するにはオブジェクトの現在の参照カウントします。

**! Wudfext.wudfobject**拡張機能では、コールバック関数もが表示され、コンテキスト オブジェクトをドライバーに関連付けられている各フレームワーク オブジェクトおよび framework オブジェクトの種類の決定が試行されます。 この最後の機能は、特定のコンパイラでは動作しません。

いくつかの例を次に示します。 最初の例では、 [ **! wudfext.umdevstacks** ](-wudfext-umdevstack.md) 0x03050E70 は、デバイス オブジェクトのアドレスからこのアドレスに渡されますと **! wudfext.wudfobject**します。 0x1 フラグは、このオブジェクトのすべての子を表示するためにします。

```dbgcmd
0: kd> !umdevstacks 
Number of device stacks: 1
  Device Stack: 0x038f6f08    Pdo Name: \Device\USBPDO-11
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: WUDFOsrUsbFx2
      UMDriver Image Path: D:\Windows\system32\DRIVERS\UMDF\WUDFOsrUsbFx2.dll
      Fx Driver: IWDFDriver 0x3044ff0
      Fx Device: IWDFDevice 0x3050e70
        IDriverEntry: WUDFOsrUsbFx2!CMyDriver 0x0303eff8
      Open UM files (use !umfile <addr> for details): 
        0x049baf84
      Device XFerMode: CopyImmediately RW: Buffered CTL: Buffered
      Object Tracker Address: 0x00000000
        Object   Tracking OFF
        Refcount Tracking OFF
    DevStack XFerMode: CopyImmediately RW: Buffered CTL: Buffered

0: kd> !wudfobject 0x3050e70 1 
IWDFDevice 0x3050e70 Fx: 0x3050e30 [Ref 2]
  15 Children
    00: IWDFIoTarget 0x3056f90 Fx: 0x3056f50 [Ref 3]
        No Children
    01: <Internal>
    02: <Internal>
    03: <Internal>
    04: IWDFIoQueue 0x305ae98 Fx: 0x305ae58 [Ref 8]
        No Children
    05: IWDFIoQueue 0x305ee98 Fx: 0x305ee58 [Ref 2]
        No Children
    06: IWDFIoQueue 0x3060e98 Fx: 0x3060e58 [Ref 2]
        No Children
    07: IWDFIoTarget 0x3066f80 Fx: 0x3066f40 [Ref 2]
        1 Children
          00: IWDFUsbInterface 0x306efd8 Fx: 0x306ef98 [Ref 1]
              3 Children
                00: IWDFIoTarget 0x3074f70 Fx: 0x3074f30 [Ref 2]
                    2 Children
                      00: IWDFMemory 0x30a4ff0 Fx: 0x30a4fb0 [Ref 2]
                          No Children
                      01: IWDFMemory 0x30aaff0 Fx: 0x30aafb0 [Ref 2]
                          No Children
                01: IWDFIoTarget 0x3078f70 Fx: 0x3078f30 [Ref 1]
                    No Children
```

次の例に示します **! wudfext.wudfobject**ファイル オブジェクトを表示します。

```dbgcmd
kd> !wudfobject 0xf5060 
IWDFFile 0xf5060 Fx: 0xf4fe8 [Ref 1]
  State: Created   Parent: 0xf2f80
  No Children
```

次の例に示します **! wudfext.wudfobject**ドライバー オブジェクトを表示します。

```dbgcmd
kd> !wudfobject 0xf2db8 0x01 
IWDFDriver 0xf2db8 Fx: 0xf2d40 [Ref 2]
  Callback: (WUDFEchoDriver!CMyDriver, 0xf2c68)
  State: Created   Parent: 0
  1 Children:
    00: IWDFDevice 0xf2f80 Fx: 0xf2f08 [Ref 2]
        State: Created   Parent: 0xf2db8
        5 Children:
          00: IWDFIoTarget 0xf33c0 Fx: 0xf3348 [Ref 3]
              State: Created   Parent: 0xf2f80
              No Children
          01: IWDFIoQueue 0xf3500 Fx: 0xf3488 [Ref 3]
              State: Created   Parent: 0xf2f80
              No Children
          02: IWDFFile 0xf5060 Fx: 0xf4fe8 [Ref 1]
              State: Created   Parent: 0xf2f80
              No Children
          03: IWDFFile 0xf5100 Fx: 0xf5088 [Ref 101]
              State: Created   Parent: 0xf2f80
              No Children
          04: IWDFFile 0xf51a0 Fx: 0xf5128 [Ref 101]
              State: Created   Parent: 0xf2f80
              No Children
```

 

 





