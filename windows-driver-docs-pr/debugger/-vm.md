---
title: vm
description: Vm 拡張機能には、ターゲットシステムの仮想メモリ使用統計に関する概要情報が表示されます。
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
ms.openlocfilehash: eaaa9cf742780e9f186c9eded8a13a777d7899f1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025160"
---
# <a name="vm"></a>!vm


**! Vm**拡張機能には、ターゲットシステムの仮想メモリ使用統計に関する概要情報が表示されます。

```dbgcmd
!vm [Flags]
```

## <a name="span-idddk__vm_dbgspanspan-idddk__vm_dbgspanparameters"></a><span id="ddk__vm_dbg"></span><span id="DDK__VM_DBG"></span>パラメータ


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
このコマンドの出力に表示される情報を指定します。 これには、次のビットの合計を指定できます。 既定値は0です。これにより、システム全体の仮想メモリ統計と、各プロセスのメモリ統計情報が表示されます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示でプロセス固有の統計を省略します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示にメモリ管理スレッドスタックを含めます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ターミナルサーバーのメモリ使用量が表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
表示にページファイル書き込みログを含めます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
表示に、ワーキングセット所有者のスレッドスタックが含まれるようにします。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>ビット 5 (0x20)  
(Windows Vista 以降)ディスプレイにカーネル仮想アドレスの使用法が含まれるようにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

|       |                  |
|-------|------------------|
| モード | カーネルモードのみ |

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[ **! Memusage**](-memusage.md)拡張コマンドを使用すると、物理メモリの使用量を分析できます。 メモリ管理の詳細については、「 *Microsoft Windows の内部*」 (Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

*フラグ*が1の場合に生成される短い出力の例を次に示します。

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

すべてのメモリ使用量は、ページとキロバイト単位で表示されます。 この表示には、次のような最も役に立つ情報が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">引き</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>物理メモリ</strong></p></td>
<td align="left"><p>システム内の合計物理メモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>利用可能なページ</strong></p></td>
<td align="left"><p>システムで使用可能なメモリのページ数 (仮想と物理の両方)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>非ページプールの使用</strong></p></td>
<td align="left"><p>非ページプールに割り当てられたページの量。 非ページプールは、ページングファイルにスワップアウトできないメモリであるため、常に物理メモリを占有する必要があります。 この数値が大きすぎる場合、通常は、システム内のどこかにメモリリークが発生していることを示します。</p></td>
</tr>
</tbody>
</table>

 

 

 





