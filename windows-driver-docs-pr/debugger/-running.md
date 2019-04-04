---
title: 実行しています。
description: 実行中の拡張機能では、ターゲット コンピューターのすべてのプロセッサで実行中のスレッドの一覧が表示されます。
ms.assetid: 08fd9806-36e9-4589-bf92-87dc02efebac
keywords:
- Windows のデバッグを実行しています。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- running
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be23896e3bb75514251c78d37c3e5359400aed6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549150"
---
# <a name="running"></a>! を実行しています。


**! を実行している**拡張機能は、ターゲット コンピューターのすべてのプロセッサで実行中のスレッド一覧を表示します。

```dbgcmd
!running [-i] [-t]
```

## <a name="span-idddkrunningdbgspanspan-idddkrunningdbgspanparameters"></a><span id="ddk__running_dbg"></span><span id="DDK__RUNNING_DBG"></span>パラメーター


<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
アイドル状態のプロセッサが、表示をによりします。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
プロセッサごとに表示されるスタック トレースを発生します。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

マルチプロセッサ コンピューターのデバッグの詳細については、[マルチプロセッサ構文](multiprocessor-syntax.md)を参照してください。

<a name="remarks"></a>注釈
-------

オプションなしで **! を実行している**アクティブなすべてのプロセッサとアイドル状態のすべてのプロセッサのアフィニティが表示されます。 すべてのアクティブなプロセッサのプロセス制御ブロック (PRCB) および 16 の組み込みのキューに置かれたスピン ロックの状態、現在および次のスレッドのフィールドも表示されます。

マルチプロセッサ Itanium システムから例を次に示します。

```dbgcmd
0: kd> !running
 
System Processors 3 (affinity mask)
 Idle Processors 0
 
     Prcb              Current           Next
  0  e0000000818f8000  e0000000818f9e50  e0000000866f12f0  ................
 1  e000000086f16010  e00000008620ebe0  e000000086eddbc0  .O..............
```

各行の最後に 16 文字では、組み込みのキューに置かれたスピン ロック (、PRCB で LockQueue エントリ) を示します。 ピリオド (します。 ) ロックが、使用されていないことを示します**O**このプロセッサにより、ロックを所有していることを意味し、 **W**ロック、プロセッサがキューに置かれたことを意味します。 詳細については、スピン ロック キューを表示する[ **! qlocks**](-qlocks.md)します。

スタック トレースと共に、アクティブでアイドル状態のプロセッサを示す例を次に示します。

```dbgcmd
0: kd> !running -it
 
System Processors f (affinity mask)
  Idle Processors f
All processors idle.
 
     Prcb      Current   Next
  0  ffdff120  805495a0            ................
 
ChildEBP RetAddr
8053e3f0 805329c2 nt!RtlpBreakWithStatusInstruction
8053e3f0 80533464 nt!_KeUpdateSystemTime+0x126
ffdff980 ffdff980 nt!KiIdleLoop+0x14
 
 1  f87e0120  f87e2e60            ................
 
ChildEBP RetAddr
f87e0980 f87e0980 nt!KiIdleLoop+0x14
 
 2  f87f0120  f87f2e60            ................
 
ChildEBP RetAddr
f87f0980 f87f0980 nt!KiIdleLoop+0x14
 
  3  f8800120  f8802e60            ................
 
ChildEBP RetAddr
f8800980 f8800980 nt!KiIdleLoop+0x14
```

 

 





