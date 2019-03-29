---
title: runaway
description: ランナウェイの拡張機能には、各スレッドで使用される時間についての情報が表示されます。
ms.assetid: ea318d5b-60c6-4d1c-80c7-6bc418ad01ab
keywords:
- ランナウェイ Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- runaway
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe8f7959412c2fa413f9ad1f448029d13823ad8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578081"
---
# <a name="runaway"></a>!runaway


**! ランナウェイ**拡張機能は、各スレッドで使用された時間に関する情報を表示します。

```dbgcmd
!runaway [Flags]
```

## <a name="span-idddkrunawaydbgspanspan-idddkrunawaydbgspanparameters"></a><span id="ddk__runaway_dbg"></span><span id="DDK__RUNAWAY_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は 0x1 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
原因のデバッガーが各スレッドで使用されたユーザー時間の量を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
原因のデバッガーが各スレッドで使用されたカーネル時間の量を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
原因のデバッガーが各スレッドが作成されてから経過した時間の量を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

**! ランナウェイ**拡張機能は、ライブ デバッグ中に、またはによって作成されたクラッシュ ダンプ ファイルをデバッグするときにのみ使用できます[ **.dump/mt** ](-dump--create-dump-file-.md)または **.dump/ma**.

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドがユーザー モードについては、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。 プロセスとスレッドの分析に関する詳細については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

この拡張機能は、どのスレッドをスピン コントロールからまたは CPU 時間がかかりすぎるの消費を確認する簡単な方法を示します。

表示では、各スレッドのスレッドの ID は 16 進数と、デバッガーの内部スレッド番号によって識別します。 デバッガーの Id も表示されます。

以下に例を示します。

```dbgcmd
0:001> !runaway 7

 User Mode Time
 Thread       Time
 0:55c        0:00:00.0093
 1:1a4        0:00:00.0000

 Kernel Mode Time
 Thread       Time
 0:55c        0:00:00.0140
 1:1a4        0:00:00.0000

 Elapsed Time
 Thread       Time
 0:55c        0:00:43.0533
 1:1a4        0:00:25.0876
```

 

 





