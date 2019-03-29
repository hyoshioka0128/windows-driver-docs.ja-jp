---
title: PoolMon の表示
description: PoolMon の表示
ms.assetid: 1dee4331-a508-4e7f-b621-4d22f6572aec
keywords:
- PoolMon の WDK を表示します
- メモリ プール モニタの WDK を表示します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5171528fd8506c333c02338b5b4144d037778489
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578883"
---
# <a name="poolmon-display"></a>PoolMon の表示


## <span id="ddk_poolmon_display_tools"></span><span id="DDK_POOLMON_DISPLAY_TOOLS"></span>


PoolMon は、コマンド ウィンドウで、プールのメモリ割り当てに関するデータの列を表示します。 方向キー、PAGEUP、PAGEDOWN キーを使用して、データをスクロールします。

**注**  PoolMon 表示全体を表示するには、コマンド プロンプト ウィンドウのサイズが 80 以上の文字幅をある必要があります (幅 = 80)、少なくとも 53 行の高さ (高さ = 53); コマンド プロンプト ウィンドウのバッファーは少なくとも 500 文字分の幅 (幅である必要があります500 を =)、少なくとも 2000 行の高さ (高さ = 2000)。 それ以外の場合、表示は切り捨てられます。

 

次の表では、PoolMon 表示内の列について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列名</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>タグ</strong></p></td>
<td align="left"><p>プールの割り当てに割り当てられた 4 バイトのタグ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>型</strong></p></td>
<td align="left"><p>かどうか、メモリの割り当ては、ページまたは非ページ バイトには。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>回数</strong></p></td>
<td align="left"><p>割り当ての数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>前回の更新以降の割り当ての数に変更します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>解放</strong></p></td>
<td align="left"><p>無料の操作の数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>前回の更新以降の割り当ての数に変更します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>相違点</strong></p></td>
<td align="left"><p>無料の操作の数-割り当ての数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>バイト数</strong></p></td>
<td align="left"><p>使用されるバイトの割り当てのサイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>前回の更新以降の割り当てサイズの変更。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Alloc ごと</strong></p></td>
<td align="left"><p>相違の値を除算してバイト単位の値</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Mapped_Driver</strong></p></td>
<td align="left"><p>ローカルのドライバー (<strong>/c</strong>) ドライバーとシステム コンポーネント頻繁に使用し、(<strong>/g</strong>) プール タグの値を割り当てることです。 この列は、使用する場合のみ表示されます、 <strong>/c</strong>または<strong>/g</strong>パラメーター。</p></td>
</tr>
</tbody>
</table>

 

次のサンプル PoolMon 出力は、割り当ての数によって並べ替えられます。 (このように、ディスプレイを並べ替え、開始と PoolMon、 **/a**パラメーターです)。

```
 Memory:  260620K Avail:   96364K  PageFlts:     0   InRam Krnl: 1916K P:17856K
 Commit: 203500K Limit: 640916K Peak: 260632K            Pool N: 8332K P:27220K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Wait Nonp    3971107 (   0)   3971077 (   0)       30    8456 (     0)    281
 ObSt Nonp    2791258 (   0)   2791258 (   0)        0       0 (     0)      0
 Gxlt Paged   1161638 (   0)   1161630 (   0)        8     864 (     0)    108
 Ustm Paged   1088342 (   0)   1088298 (   0)       44    2464 (     0)     56
 Io   Nonp    1021112 (   1)   1020985 (   1)      127   91912 (     0)    723
 ObSq Paged    967615 (   0)    967615 (   0)        0       0 (     0)      0
 Key  Paged    954821 (   0)    953979 (   0)      842   87528 (     0)    103
 SePa Nonp     680348 (   0)    680321 (   0)       27    3656 (     0)    135
```

### <a name="span-idupdateratespanspan-idupdateratespanspan-idupdateratespanupdate-rate"></a><span id="Update_Rate"></span><span id="update_rate"></span><span id="UPDATE_RATE"></span>更新間隔

PoolMon では、5 秒ごとの表示を更新します。 更新間隔を変更することはできません。

### <a name="span-idaccumulatedvaluesspanspan-idaccumulatedvaluesspanspan-idaccumulatedvaluesspanaccumulated-values"></a><span id="Accumulated_Values"></span><span id="accumulated_values"></span><span id="ACCUMULATED_VALUES"></span>累積値

PoolMon を表示するデータが収集され、プールのタグ付けを有効にするたびに、Windows によって計算されます。 割り当て、解放操作は、使用されているバイトの値は、Windows が起動された時間から蓄積し、Windows が再起動されるまで 1 ずつ増加します。 Windows が既に開始後に、ドライバーまたはコンポーネントが開始されると場合、は、値が前回開始し、リセット、ドライバーまたはシステムを再起動したときにのみ、ドライバーまたはコンポーネントの蓄積されます。

### <a name="span-idinterpretingtagvaluesspanspan-idinterpretingtagvaluesspanspan-idinterpretingtagvaluesspaninterpreting-tag-values"></a><span id="Interpreting_Tag_Values"></span><span id="interpreting_tag_values"></span><span id="INTERPRETING_TAG_VALUES"></span>タグの値を解釈します。

プールのすべてのメモリ割り当ては、タグがすべてが特徴的なタグの値。 プールのメモリ割り当てが、メモリの割り当て、ドライバーを使用して、タグの値を設定するときに、特性のタグの値を持つ[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)または[ **ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)します。 ドライバーをタグの値を割り当てない場合 ([**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)、 [ **ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506))、Windows がまだですが、タグを作成します[なし] の既定のタグ値を割り当てます。 その結果、他のプール割り当てのドライバーの割り当ての統計情報を区別できません。

 

 





