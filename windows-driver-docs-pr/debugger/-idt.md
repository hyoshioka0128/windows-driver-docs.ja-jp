---
title: idt
description: Idt 拡張機能では、指定した割り込みディスパッチ テーブル (IDT) の割り込みサービス ルーチン (Isr) が表示されます。
ms.assetid: 6b289fde-85a3-4a40-8354-db6861ca8cb2
keywords:
- ISR (割り込みサービス ルーチン)
- IDT (割り込みディスパッチ テーブル)
- Windows デバッグ idt
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- idt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c65570198a00701ea15c301c1afeb15ed535525b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580403"
---
# <a name="idt"></a>!idt


**! Idt**拡張機能では、指定した割り込みディスパッチ テーブル (IDT) の割り込みサービス ルーチン (Isr) が表示されます。

```dbgcmd
!idt IDT 
!idt [-a] 
!idt -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______IDT______"></span><span id="_______idt______"></span> *IDT*   
表示する IDT を指定します。

<span id="_______-a______"></span><span id="_______-A______"></span> **-**   
ときに*IDT*が指定されていない、デバッガーが省略された形式でターゲット コンピューター上のすべてのプロセッサ IDTs を表示します。 場合 **-a**を指定すると、各 IDT の Isr も表示されます。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能のコマンドは、x64 ベースまたは x86 ベースの対象コンピューターにのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Isr を特定および IDTs については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

Itanium のターゲット コンピューターでの割り込みのベクター テーブルを表示する方法の詳細については、次を参照してください。 [ **! ivt**](-ivt.md)します。

<a name="remarks"></a>コメント
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !idt

Dumping IDT:

37:806ba78c hal!PicSpuriousService37
3d:806bbc90 hal!HalpApcInterrupt
41:806bbb04 hal!HalpDispatchInterrupt
50:806ba864 hal!HalpApicRebootService
63:8641376c VIDEOPRT!pVideoPortInterrupt (KINTERRUPT 86413730)
73:862aa044 portcls!CInterruptSyncServiceRoutine (KINTERRUPT 862aa008)
82:86594314 atapi!IdePortInterrupt (KINTERRUPT 865942d8)
83:86591bec SCSIPORT!ScsiPortInterrupt (KINTERRUPT 86591bb0)
92:862b53dc serial!SerialCIsrSw (KINTERRUPT 862b53a0)
93:86435844 i8042prt!I8042KeyboardInterruptService (KINTERRUPT 86435808)
a3:863b366c i8042prt!I8042MouseInterruptService (KINTERRUPT 863b3630)
a4:8636bbec USBPORT!USBPORT_InterruptService (KINTERRUPT 8636bbb0)
b1:86585bec ACPI!ACPIInterruptServiceRoutine (KINTERRUPT 86585bb0)
b2:863c0524 serial!SerialCIsrSw (KINTERRUPT 863c04e8)
b4:86391a54 NDIS!ndisMIsr (KINTERRUPT 86391a18)
         USBPORT!USBPORT_InterruptService (KINTERRUPT 863ae890)
c1:806ba9d0 hal!HalpBroadcastCallService
d1:806b9dd4 hal!HalpClockInterrupt
e1:806baf30 hal!HalpIpiHandler
e3:806baca8 hal!HalpLocalApicErrorService
fd:806bb460 hal!HalpProfileInterrupt
```

 

 





