---
title: ivt
description: Ivt 拡張機能は、Itanium の割り込みのベクター テーブルを表示します。
ms.assetid: 855c50ed-361e-4236-a1b0-e1b2a3ae2a62
keywords:
- 割り込みのベクター テーブル
- Windows デバッグ ivt
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ivt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2003c3fa260f835673cf4277f10156d73c4b6cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556641"
---
# <a name="ivt"></a>! ivt


! Ivt 拡張機能は、Itanium の割り込みのベクター テーブルを表示します。

```dbgcmd
!ivt [-v] [-a] [Vector] 
!ivt -? 
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Vector______"></span><span id="_______vector______"></span><span id="_______VECTOR______"></span> *ベクター*   
現在のプロセッサの割り込みのベクター テーブル エントリを指定します。 場合*ベクター*は省略すると、ターゲット コンピューターの現在のプロセッサの割り込みの全体のベクター テーブルが表示されます。 しない限り、割り当てられていないベクトルの割り込みが表示されない、 **-a**オプションを指定します。

<span id="_______-a______"></span><span id="_______-A______"></span> **-**   
割り当て済みでないものも含め、すべてのベクトルの割り込みを表示します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細出力を表示します。

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

 

この拡張機能のコマンドは、Itanium のターゲット コンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

X64 または x86 のターゲット コンピューター上の割り込みのディスパッチ テーブルを表示する方法の詳細については、[ **! idt**](-idt.md)を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !ivt

Dumping IA64 IVT:

00:e000000083005f60 nt!KiPassiveRelease
0f:e000000083576830 hal!HalpPCIISALine2Pin
10:e0000000830067f0 nt!KiApcInterrupt
20:e000000083006790 nt!KiDispatchInterrupt
30:e000000083576b30 hal!HalpCMCIHandler
31:e000000083576b20 hal!HalpCPEIHandler
41:e000000085039680 i8042prt!I8042KeyboardInterruptService (KINTERRUPT e000000085039620)
51:e000000085039910 i8042prt!I8042MouseInterruptService (KINTERRUPT e0000000850398b0)
61:e0000000854484f0 VIDEOPRT!pVideoPortInterrupt (KINTERRUPT e000000085448490)
71:e0000000856c9450 NDIS!ndisMIsr (KINTERRUPT e0000000856c93f0)
81:e0000000857fd000 SCSIPORT!ScsiPortInterrupt (KINTERRUPT e0000000857fcfa0)
91:e0000000857ff510 atapi!IdePortInterrupt (KINTERRUPT e0000000857ff4b0)
a1:e0000000857d84b0 atapi!IdePortInterrupt (KINTERRUPT e0000000857d8450)
a2:e0000165fff2cab0 portcls!CInterruptSyncServiceRoutine (KINTERRUPT e0000165fff2ca50)
b1:e0000000858c7460 ACPI!ACPIInterruptServiceRoutine (KINTERRUPT e0000000858c7400)
b2:e0000000850382e0 USBPORT!USBPORT_InterruptService (KINTERRUPT e000000085038280)
d0:e0000000835768d0 hal!HalpClockInterrupt
e0:e000000083576850 hal!HalpIpiInterruptHandler
f0:e0000000835769c0 hal!HalpProfileInterrupt
f1:e000000083576830 hal!HalpPCIISALine2Pin
fd:e000000083576b10 hal!HalpMcRzHandler
fe:e000000083576830 hal!HalpPCIISALine2Pin
```

 

 





