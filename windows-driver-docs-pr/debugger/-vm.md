---
title: vm
description: Vm 拡張機能は、ターゲット システム上の仮想メモリの使用の統計に関する概要情報を表示します。
ms.assetid: 25e4f80c-d4ca-407c-991d-e8ee5dfbb309
keywords:
- vm の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb4ae55dd673f84744b856e7154b9e8b2b1158c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571760"
---
# <a name="vm"></a>!vm


**! Vm**拡張機能では、ターゲット システムの仮想メモリの使用の統計に関する概要情報が表示されます。

```dbgcmd
!vm [Flags]
```

## <a name="span-idddkvmdbgspanspan-idddkvmdbgspanparameters"></a><span id="ddk__vm_dbg"></span><span id="DDK__VM_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
このコマンドの出力で表示する情報を指定します。 これは、次のビットの任意の合計を指定できます。 既定値は、0 で、システム全体の仮想メモリの統計情報と各プロセスのメモリ統計情報が表示されます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
プロセス固有の統計情報を省略するためにディスプレイをによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
メモリ管理スレッド スタックが表示をによりします。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ターミナル サーバーのメモリ使用量が表示をによりします。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
ページのファイル書き込みログが表示をによりします。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
作業セットの所有者のスレッドのスタックが表示をによりします。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
(Windows Vista 以降)カーネルの仮想アドレスの使用状況が表示をによりします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

|       |                  |
|-------|------------------|
| モード | カーネル モードのみ |

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[ **! Memusage** ](-memusage.md)物理メモリ使用量を分析する拡張機能のコマンドを使用できます。 メモリ管理の詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

ときに生成される短い出力の例を次に示します*フラグ*1 には。

```dbgcmd
kd> !vm 1

*** Virtual Memory Usage ***
      Physical Memory:     16270   (   65080 Kb)
      Page File: \??\E:\pagefile.sys
         Current:     98304Kb Free Space:     61044Kb
 Minimum:     98304Kb Maximum:       196608Kb
      Available Pages:      5543   (   22172 Kb)
      ResAvail Pages:       6759   (   27036 Kb)
      Locked IO Pages:       112   (     448 Kb)
 Free System PTEs:    45089   (  180356 Kb)
      Free NP PTEs:         5145   (   20580 Kb)
      Free Special NP:       336   (    1344 Kb)
      Modified Pages:        714   (    2856 Kb)
      NonPagedPool Usage:    877   (    3508 Kb)
      NonPagedPool Max:     6252   (   25008 Kb)
      PagedPool 0 Usage:     729   (    2916 Kb)
      PagedPool 1 Usage:     432   (    1728 Kb)
      PagedPool 2 Usage:     436   (    1744 Kb)
      PagedPool Usage:      1597   (    6388 Kb)
      PagedPool Maximum:   13312   (   53248 Kb)
      Shared Commit:        1097   (    4388 Kb)
      Special Pool:          229   (     916 Kb)
      Shared Process:       1956   (    7824 Kb)
      PagedPool Commit:     1597   (    6388 Kb)
      Driver Commit:         828   (    3312 Kb)
      Committed pages:     21949   (   87796 Kb)
      Commit limit:        36256   (  145024 Kb)
```

すべてのメモリ (キロバイト単位) とページの使用が一覧表示します。 この表示で最も有用な情報は次のです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>物理メモリ</strong></p></td>
<td align="left"><p>システムの物理メモリの合計。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>使用可能なページ</strong></p></td>
<td align="left"><p>システム、仮想および物理の両方で使用できるメモリのページの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>非ページ プールの使用率</strong></p></td>
<td align="left"><p>非ページ プールに割り当てられたページの量。 非ページ プールでは、メモリ スワップ アウトできません、ページング ファイルにも常に物理メモリを使用する必要がありますのでです。 この数が多すぎて、メモリ リークどこかでがシステムを示す値を通常、これは。</p></td>
</tr>
</tbody>
</table>

 

 

 





