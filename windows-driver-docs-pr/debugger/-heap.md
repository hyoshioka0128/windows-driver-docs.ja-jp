---
title: ヒープ
description: ヒープ拡張機能では、ヒープの使用状況に関する情報の表示、ヒープマネージャーでのブレークポイントの制御、リークしたヒープブロックの検出、ヒープブロックの検索、またはページヒープ情報の表示を行います。
ms.assetid: 70947b56-1a8c-4e78-85d0-d5df87f3150c
keywords:
- ヒープ使用量
- GFlags、ページヒープの有効化
- ヒープ Windows デバッグ
ms.date: 08/23/2019
topic_type:
- apiref
api_name:
- heap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ffc629793b5dba6561f6b6dfda7af6b68558141
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025238"
---
# <a name="heap"></a>!heap


**! Heap**拡張機能では、ヒープ使用量の情報の表示、ヒープマネージャーでのブレークポイントの制御、リークしたヒープブロックの検出、ヒープブロックの検索、またはページヒープ情報の表示を行います。

この拡張機能は、セグメントヒープと NT ヒープをサポートします。 すべてのヒープとその型を一覧表示するには、パラメーターを指定せずに! heap を使用します。

```dbgcmd
!heap [HeapOptions] [ValidationOptions] [Heap] 
!heap -b [{alloc|realloc|free} [Tag]] [Heap | BreakAddress] 
!heap -B {alloc|realloc|free} [Heap | BreakAddress] 
!heap -l 
!heap -s [SummaryOptions] [StatHeapAddress] 
!heap -i HeapAddress
!heap -x [-v] Address 
!heap -p [PageHeapOptions] 
!heap -srch [Size] Pattern
!heap -flt FilterOptions
!heap -stat [-h Handle [-grp GroupBy [MaxDisplay]]]
!heap [-p] -?
!heap -triage [Handle | Address] 
```

## <a name="span-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspansegment-and-nt-heap-parameters"></a><span id="Segment_and_NT_Heap_Parameters"></span><span id="segment_and_nt_heap_parameters"></span><span id="SEGMENT_AND_NT_HEAP_PARAMETERS"></span>セグメントおよび NT ヒープパラメーター


これらのパラメーターは、セグメントおよび NT ヒープで動作します。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
概要情報を要求することを指定します。 場合、summary*オプション*と指定した場合は、現在のプロセスに関連付けられているすべてのヒープの概要情報が表示されます。

<span id="_______SummaryOptions______"></span><span id="_______summaryoptions______"></span><span id="_______SUMMARYOPTIONS______"></span>概要*オプション*   
には、次のオプションの任意の組み合わせを指定できます。 [概要 *] オプション*では、大文字と小文字は区別されません。 「! Heap-s-?」と入力します。 を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>すべてのデータブロックを検証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong> <em>BucketSize</em></p></td>
<td align="left"><p>バケットのサイズを指定します。 既定値は1024ビットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong> <em>Dumpblocksize</em></p></td>
<td align="left"><p>バケットのサイズを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>すべてのヒープブロックをダンプします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>各ブロックの内容を表示することを指定します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-triage__Handle___Address___"></span><span id="_______-triage__handle___address___"></span><span id="_______-TRIAGE__HANDLE___ADDRESS___"></span> **-トリアージ\[** <em>ハンドル</em>アドレス **|** **\]**    
デバッガーがプロセスのヒープ内のエラーを自動的に検索します。 ヒープハンドルが引数として指定されている場合、そのヒープが検査されます。それ以外の場合は、指定されたアドレスを含むすべてのヒープが検索され、見つかった場合は検査されます。 **-トリアージ**を使用するのは、低断片化ヒープ (lfh) の破損を検証する唯一の方法です。

<span id="_______-x_-v_"></span><span id="_______-X_-V_"></span> **-x** **** -v \[\]   
指定されたアドレスを含むヒープブロックをデバッガーが検索します。 -V を追加すると、コマンドは、現在のプロセスの仮想メモリ領域全体で、このヒープブロックへのポインターを検索します。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
デバッガーがリークしたヒープブロックを検出するようにします。

<span id="_______-i________Address______-h_HeapAddress______"></span><span id="_______-i________address______-h_heapaddress______"></span><span id="_______-I________ADDRESS______-H_HEAPADDRESS______"></span> **-i**  ****  *アドレス* **-h** *HeapAddress*    
指定した*ヒープ*に関する情報を表示します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
検索するアドレスを指定します。

<span id="_______-_______"></span> **-?**    
デバッガーコマンドウィンドウにこの拡張機能の簡単なヘルプテキストを表示します。 **! Heap-?** を使用します。 一般的なヘルプと **! heap-p-?** ページヒープのヘルプを参照してください。

## <a name="span-idddk__heap_dbgspanspan-idddk__heap_dbgspannt-heap-parameters"></a><span id="ddk__heap_dbg"></span><span id="DDK__HEAP_DBG"></span>NT ヒープパラメーター


これらのパラメーターは、NT ヒープでのみ機能します。

<span id="_______HeapOptions______"></span><span id="_______heapoptions______"></span><span id="_______HEAPOPTIONS______"></span>*Heapoptions*   
には、次のオプションの任意の組み合わせを指定できます。 *Heapoptions*値では大文字と小文字が区別されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>指定されたヒープをデバッガーが検証します。</p>
<div class="alert">
<strong></strong>注  このオプションでは、低い断片化ヒープ (lfh) の破損は検出されません。 代わりに<strong>-トリアージ</strong>を使用してください。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>指定したヒープのすべての情報が表示されます。 この場合のサイズは、ヒープの粒度に切り上げられます。 (を実行すると、 <strong>-a</strong>オプションを指定して実行することは、3つのオプションを使用して実行することと同じです。 <strong>-h-f-m</strong>には時間がかかることがあります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-h</strong></p></td>
<td align="left"><p>指定されたヒープのすべての LFH 以外のエントリを表示に含めます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-hl</strong></p></td>
<td align="left"><p>指定したヒープのすべてのエントリ (LFH エントリを含む) が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-f</strong></p></td>
<td align="left"><p>指定されたヒープのすべてのフリーリストエントリを表示に含めます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong></p></td>
<td align="left"><p>指定されたヒープのすべてのセグメントエントリを表示に含めます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>指定したヒープのタグ情報を表示に含めます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-T</strong></p></td>
<td align="left"><p>指定されたヒープの疑似タグエントリを表示に含めます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-g</strong></p></td>
<td align="left"><p>表示にグローバルタグ情報が含まれるようにします。 グローバルタグは、タグなしの各割り当てに関連付けられています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>指定したヒープの概要情報を表示に含めます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-k</strong></p></td>
<td align="left"><p>(x86 ベースのターゲットのみ)各エントリに関連付けられているスタックバックトレースを表示に含めます。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ValidationOptions______"></span><span id="_______validationoptions______"></span><span id="_______VALIDATIONOPTIONS______"></span>*Validationoptions*   
次のオプションのいずれか1つを指定できます。 *Validationoptions*では大文字と小文字が区別されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-D</strong></p></td>
<td align="left"><p>指定されたヒープの呼び出しの検証を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-E</strong></p></td>
<td align="left"><p>指定したヒープに対する呼び出しの検証を有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>指定したヒープのヒープチェックを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>指定したヒープのヒープチェックを有効にします。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-i________Heap_Address______or_HeapAddress______"></span><span id="_______-i________heap_address______or_heapaddress______"></span><span id="_______-I________HEAP_ADDRESS______OR_HEAPADDRESS______"></span> **-i**  ****  *ヒープ*  ****  *アドレス* **または** *HeapAddress*   
指定した*ヒープ*に関する情報を表示します。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span>*Breakaddress*   
ブレークポイントを設定または削除するブロックのアドレスを指定します。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
デバッガーによって、ヒープマネージャーで条件付きブレークポイントが作成されます。 **-B**オプションの後には、 **alloc**、 **realloc**、または**free**を指定できます。メモリの割り当て、再割り当て、または解放によってブレークポイントをアクティブにするかどうかを指定します。 *Breakaddress*を使用してブロックのアドレスを指定した場合は、ブレークポイントの種類を省略できます。 ヒープアドレスまたはヒープインデックスを指定するために*ヒープ*を使用する場合は、*タグ*パラメーターに加えて、型を含める必要があります。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span>*タグ*   
ヒープ内のタグ名を指定します。

<span id="_______-B______"></span><span id="_______-b______"></span> **-B**   
デバッガーによって、ヒープマネージャーから条件付きブレークポイントが削除されます。 ブレークポイントの種類 (**alloc**、 **realloc**、または**free**) を指定する必要があり、 **-b**オプションで使用されているものと同じである必要があります。

<span id="_______StatHeapAddress______"></span><span id="_______statheapaddress______"></span><span id="_______STATHEAPADDRESS______"></span>すべての*ip アドレス*   
ヒープのアドレスを指定します。 0または省略した場合は、現在のプロセスに関連付けられているすべてのヒープが表示されます。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
ページヒープ情報が要求されていることを指定します。 このオプションを使用して*Pageheapoptions*を指定しない場合は、すべてのページヒープが表示されます。

<span id="_______PageHeapOptions______"></span><span id="_______pageheapoptions______"></span><span id="_______PAGEHEAPOPTIONS______"></span>*Pageheapoptions*   
次のオプションのいずれか1つを指定できます。 *Pageheapoptions*では大文字と小文字が区別されます。 オプションが指定されていない場合、使用可能なすべてのページヒープハンドルが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-h</strong> <em>ハンドル</em></p></td>
<td align="left"><p>デバッガーで、ハンドル<em>ハンドル</em>を持つページヒープに関する詳細情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong> <em>アドレス</em></p></td>
<td align="left"><p>デバッガーが、ブロックに<em>アドレス</em>を含むページヒープを検索します。 このアドレスがページヒープの一部であるかどうか、ブロック内のオフセット、ブロックが割り当てられているか解放されたかなど、このアドレスがフルページヒープブロックにどのように関連しているかの詳細が含まれます。 スタックトレースは、使用可能な場合は常に含まれます。 このオプションを使用する場合、サイズは、ヒープ割り当ての粒度の倍数で表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong>[<strong>c</strong>|<strong>s</strong>] [<em>トレース</em>]</p></td>
<td align="left"><p>大量のヒープユーザーの収集されたトレースをデバッガーに表示させます。 <em>トレース</em>は、表示するトレースの数を指定します。既定値は4です。 指定した数よりも多くのトレースがある場合は、最も古いトレースが表示されます。 <strong>-T</strong>または<strong>-tc</strong>が使用されている場合、トレースは count usage で並べ替えられます。 <strong>-Ts</strong>を使用する場合、トレースはサイズ順に並べ替えられます。 ( <strong>-Tc</strong>オプションと<strong>-Ts</strong>オプションは windows xp でのみサポートされています。 <strong>-t</strong>オプションは、windows xp およびそれ以前のバージョンの windows でのみサポートされています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-fi</strong> [<em>トレース</em>]</p></td>
<td align="left"><p>デバッガーが最新のフォールト挿入トレースを表示します。 <em>トレース</em>は、表示する数量を指定します。既定値は4です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-すべて</strong></p></td>
<td align="left"><p>デバッガーですべてのページヒープに関する詳細情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-?</strong></p></td>
<td align="left"><p>ヒープブロックのダイアグラムを含むページヒープのヘルプを表示します。 (これらの図については、次の「解説」を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**! Heap-p**拡張コマンドを使用する前に、ターゲットプロセスに対してページヒープを有効にする必要があります。 詳細については、次の「解説」を参照してください。

<span id="_______-srch______"></span><span id="_______-SRCH______"></span> **-srch**   
指定されたパターンのすべてのヒープをスキャンします。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*パターン*   
検索するパターンを指定します。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*サイズ*   
次のオプションのいずれか1つを指定できます。 パターンのサイズを指定します。 '-' が必要です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>パターンは、1バイトのサイズです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>パターンは、1つの単語のサイズになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>パターンは、1つの DWORD サイズです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-q</strong></p></td>
<td align="left"><p>パターンは、1つの QWORD のサイズです。</p></td>
</tr>
</tbody>
</table>

 

上記のいずれも指定されていない場合、パターンはコンピューターポインターと同じサイズであると見なされます。

<span id="_______-flt______"></span><span id="_______-FLT______"></span> **-flt**   
指定されたサイズまたはサイズ範囲のヒープだけを含むように表示を制限します。

<span id="_______FilterOptions______"></span><span id="_______filteroptions______"></span><span id="_______FILTEROPTIONS______"></span>*Filteroptions*   
次のオプションのいずれか1つを指定できます。 *Filteroptions*では大文字と小文字が区別されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>s</strong> <em>サイズ</em></p></td>
<td align="left"><p>指定されたサイズのヒープだけを含むように表示を制限します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> SizeMin <em>SizeMax</em></p></td>
<td align="left"><p>指定されたサイズ範囲内のヒープのみを含むように表示を制限します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-stat______"></span><span id="_______-STAT______"></span> **-stat**   
指定したヒープの使用状況の統計情報を表示します。

<span id="_______-h________Handle______"></span><span id="_______-h________handle______"></span><span id="_______-H________HANDLE______"></span> **-h***ハンドル*   
*ハンドル*のヒープのみの使用状況の統計を表示します。 *Handle*が0であるか省略されている場合は、すべてのヒープの使用状況の統計が表示されます。

<span id="_______-grp________GroupBy______"></span><span id="_______-grp________groupby______"></span><span id="_______-GRP________GROUPBY______"></span> **-grp** ****  *GroupBy*   
*GroupBy*によって指定されたとおりに表示を並べ替えます。 *GroupBy*のオプションについては、次の表を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ある</strong></p></td>
<td align="left"><p>割り当てサイズに従って使用状況の統計情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>ブロックカウントに従って使用状況の統計情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>各割り当ての合計サイズに従って使用状況の統計情報を表示します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______MaxDisplay______"></span><span id="_______maxdisplay______"></span><span id="_______MAXDISPLAY______"></span>*Maxdisplay*   
出力を*Maxdisplay*行数のみに制限します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p></p>
Ext .dll の .dll</td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ヒープの詳細については、次のリソースを参照してください。

手順Mark Russinovich と David ソロモンによる*Microsoft Windows の内部構造*。

[例 11:ページヒープ検証の有効化](example-11---enabling-page-heap-verification.md)

[例 12:ページヒープ検証を使用したバグの検出](example-12---using-page-heap-verification-to-find-a-bug.md)

ヒープメモリプロセスロガーの使用方法の詳細につい[ては、次を参照してください。例 11:プライベートトレースセッションを開始しています](https://docs.microsoft.com/windows-hardware/drivers/devtest/example-11--starting-a-private-trace-session)

<a name="remarks"></a>コメント
-------

この拡張機能コマンドを使用すると、さまざまなタスクを実行できます。

Standard **! heap**コマンドは、現在のプロセスのヒープ情報を表示するために使用されます。 (これは、ユーザーモードプロセスでのみ使用してください。 システムプロセスには、 [ **! pool**](-pool.md) extension コマンドを使用する必要があります。)

**! Heap-b**および **! heap-b**コマンドは、ヒープマネージャーで条件付きブレークポイントを作成および削除するために使用されます。

**! Heap-l**コマンドは、リークしたヒープブロックを検出します。 ガベージコレクターアルゴリズムを使用して、プロセスアドレス空間のどこでも参照されていないすべてのビジーブロックをヒープから検出します。 大規模なアプリケーションでは、完了までに数分かかることがあります。 このコマンドは、Windows XP 以降のバージョンの Windows でのみ使用できます。

**! Heap-x**コマンドは、指定されたアドレスを含むヒープブロックを検索します。 **-V**オプションを使用した場合、このコマンドは、現在のプロセスの仮想メモリ領域全体で、このヒープブロックへのポインターを検索します。 このコマンドは、Windows XP 以降のバージョンの Windows でのみ使用できます。

**! Heap-p**コマンドは、さまざまな形式のページヒープ情報を表示します。 **! Heap-p**を使用する前に、ターゲットプロセスのページヒープを有効にする必要があります。 これは、グローバルフラグ (msbuild.exe) ユーティリティを使用して行います。 これを行うには、ユーティリティを起動して、対象アプリケーションの名前を **[イメージファイル名]** ボックスに入力し、 **[イメージファイルのオプション]** を選択して**ページヒープを有効に**し、 **[適用]** をクリックします。 または、コマンドプロンプトウィンドウで「 **gflags/i** *xxx. .exe* **+ hpa**」と入力してグローバルフラグユーティリティを起動することもできます。ここで、 *xxx*はターゲットアプリケーションの名前です。

**! Heap-p-t\[c | s\]** コマンドは、Windows XP 以降ではサポートされていません。 デバッガーパッケージに用意されている[UMDH](umdh.md)ツールを使用して、同様の結果を取得します。

**! Heap-srch**コマンドは、指定された特定のパターンを含むヒープエントリを表示します。

**! Flt**コマンドは、指定されたサイズのヒープ割り当てのみを表示するように制限します。

**! Heap-stat**コマンドでは、ヒープ使用量の統計情報が表示されます。

Standard **! heap**コマンドの例を次に示します。

```dbgcmd
0:000> !ntsdexts.heap -a
Index   Address  Name      Debugging options enabled
  1:   00250000 
    Segment at 00250000 to 00350000 (00056000 bytes committed)
    Flags:               50000062
    ForceFlags:          40000060
    Granularity:         8 bytes
    Segment Reserve:     00100000
    Segment Commit:      00004000
    DeCommit Block Thres:00000400
    DeCommit Total Thres:00002000
    Total Free Size:     000003be
    Max. Allocation Size:7ffddfff
    Lock Variable at:    00250b54
    Next TagIndex:       0012
    Maximum TagIndex:    07ff
    Tag Entries:         00350000
    PsuedoTag Entries:   00250548
    Virtual Alloc List:  00250050
    UCR FreeList:        002504d8
    128-bit bitmap of free lists
    FreeList Usage:      00000014 00000000 00000000 00000000
              Free    Free
              List    List
#       Head      Blink      Flink
    FreeList[ 00 ] at 002500b8: 002a4378 . 002a4378
                                0x02 - HEAP_ENTRY_EXTRA_PRESENT
                                0x04 - HEAP_ENTRY_FILL_PATTERN
        Entry     Prev    Cur   0x10 - HEAP_ENTRY_LAST_ENTRY

Address   Size    Size  flags
002a4370: 00098 . 01c90 [14] - free
    FreeList[ 02 ] at 002500c8: 0025cb30 . 002527b8
002527b0: 00058 . 00010 [04] - free
0025cb28: 00088 . 00010 [04] - free
    FreeList[ 04 ] at 002500d8: 00269a08 . 0026e530
0026e528: 00038 . 00020 [04] - free
0026a4d0: 00038 . 00020 [06] - free
0026f9b8: 00038 . 00020 [04] - free
0025cda0: 00030 . 00020 [06] - free
00272660: 00038 . 00020 [04] - free
0026ab60: 00038 . 00020 [06] - free
00269f20: 00038 . 00020 [06] - free
00299818: 00038 . 00020 [04] - free
0026c028: 00038 . 00020 [06] - free
00269a00: 00038 . 00020 [46] - free
 
    Segment00 at 00250b90:
Flags:           00000000
Base:            00250000
First Entry:     00250bc8
Last Entry:      00350000
Total Pages:     00000080
Total UnCommit:  00000055
Largest UnCommit:000aa000
UnCommitted Ranges: (1)
    002a6000: 000aa000

    Heap entries for Segment00 in Heap 250000
                        0x01 - HEAP_ENTRY_BUSY            
                        0x02 - HEAP_ENTRY_EXTRA_PRESENT   
                        0x04 - HEAP_ENTRY_FILL_PATTERN    
                        0x08 - HEAP_ENTRY_VIRTUAL_ALLOC   
                        0x10 - HEAP_ENTRY_LAST_ENTRY      
                        0x20 - HEAP_ENTRY_SETTABLE_FLAG1  
                        0x40 - HEAP_ENTRY_SETTABLE_FLAG2  
Entry     Prev    Cur   0x80 - HEAP_ENTRY_SETTABLE_FLAG3  

Address   Size    Size  flags       (Bytes used)    (Tag name)
00250000: 00000 . 00b90 [01] - busy (b90)
00250b90: 00b90 . 00038 [01] - busy (38) 
00250bc8: 00038 . 00040 [07] - busy (24), tail fill (NTDLL!LDR Database)
00250c08: 00040 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00250c68: 00060 . 00028 [07] - busy (10), tail fill (NTDLL!LDR Database)
00250c90: 00028 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00250cf0: 00060 . 00050 [07] - busy (38), tail fill (Objects=  80)
00250d40: 00050 . 00048 [07] - busy (2e), tail fill (NTDLL!LDR Database)
00250d88: 00048 . 00c10 [07] - busy (bf4), tail fill (Objects>1024)
00251998: 00c10 . 00030 [07] - busy (12), tail fill (NTDLL!LDR Database)
...
002525c0: 00030 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00252620: 00060 . 00050 [07] - busy (38), tail fill (NTDLL!LDR Database)
00252670: 00050 . 00040 [07] - busy (22), tail fill (NTDLL!CSRSS Client)
002526b0: 00040 . 00040 [07] - busy (24), tail fill (Objects=  64)
002526f0: 00040 . 00040 [07] - busy (24), tail fill (Objects=  64)
00252730: 00040 . 00028 [07] - busy (10), tail fill (Objects=  40)
00252758: 00028 . 00058 [07] - busy (3c), tail fill (Objects=  88)
002527b0: 00058 . 00010 [04] free fill
002527c0: 00010 . 00058 [07] - busy (3c), tail fill (NTDLL!LDR Database)
00252818: 00058 . 002d0 [07] - busy (2b8), tail fill (Objects= 720)
00252ae8: 002d0 . 00330 [07] - busy (314), tail fill (Objects= 816)
00252e18: 00330 . 00330 [07] - busy (314), tail fill (Objects= 816)
00253148: 00330 . 002a8 [07] - busy (28c), tail fill (NTDLL!LocalAtom)
002533f0: 002a8 . 00030 [07] - busy (18), tail fill (NTDLL!LocalAtom)
00253420: 00030 . 00030 [07] - busy (18), tail fill (NTDLL!LocalAtom)
00253450: 00030 . 00098 [07] - busy (7c), tail fill (BASEDLL!LMEM)
002534e8: 00098 . 00060 [07] - busy (44), tail fill (BASEDLL!TMP)
00253548: 00060 . 00020 [07] - busy (1), tail fill (Objects=  32)
00253568: 00020 . 00028 [07] - busy (10), tail fill (Objects=  40)
00253590: 00028 . 00030 [07] - busy (16), tail fill (Objects=  48)
...
0025ccb8: 00038 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
0025cd18: 00060 . 00058 [07] - busy (3c), tail fill (NTDLL!LDR Database)
0025cd70: 00058 . 00030 [07] - busy (18), tail fill (NTDLL!LDR Database)
0025cda0: 00030 . 00020 [06] free fill (NTDLL!Temporary)
0025cdc0: 00020 . 00258 [07] - busy (23c), tail fill (Objects= 600)
0025d018: 00258 . 01018 [07] - busy (1000), tail fill (Objects>1024)
0025e030: 01018 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
...
002a4190: 00028 . 00118 [07] - busy (100), tail fill (BASEDLL!GMEM)
002a42a8: 00118 . 00030 [07] - busy (18), tail fill (Objects=  48)
002a42d8: 00030 . 00098 [07] - busy (7c), tail fill (Objects= 152)
002a4370: 00098 . 01c90 [14] free fill
002a6000:      000aa000      - uncommitted bytes.
```

**! Heap-l**コマンドの例を次に示します。

```dbgcmd
1:0:011> !heap -l
1:Heap 00170000
Heap 00280000
Heap 00520000
Heap 00b50000
Heap 00c60000
Heap 01420000
Heap 01550000
Heap 016d0000
Heap 019b0000
Heap 01b40000
Scanning VM ...
## Entry     User      Heap      Segment       Size  PrevSize  Flags

001b2958  001b2960  00170000  00000000        40        18  busy extra
001b9cb0  001b9cb8  00170000  00000000        80       300  busy extra
001ba208  001ba210  00170000  00000000        80        78  busy extra
001cbc90  001cbc98  00170000  00000000        e0        48  busy extra
001cbd70  001cbd78  00170000  00000000        d8        e0  busy extra
001cbe90  001cbe98  00170000  00000000        68        48  busy extra
001cbef8  001cbf00  00170000  00000000        58        68  busy extra
001cc078  001cc080  00170000  00000000        f8       128  busy extra
001cc360  001cc368  00170000  00000000        80        50  busy extra
001cc3e0  001cc3e8  00170000  00000000        58        80  busy extra
001fe550  001fe558  00170000  00000000       150       278  busy extra
001fe6e8  001fe6f0  00170000  00000000        48        48  busy extra
002057a8  002057b0  00170000  00000000        58        58  busy extra
00205800  00205808  00170000  00000000        48        58  busy extra
002058b8  002058c0  00170000  00000000        58        70  busy extra
00205910  00205918  00170000  00000000        48        58  busy extra
00205958  00205960  00170000  00000000        90        48  busy extra
00246970  00246978  00170000  00000000        60        88  busy extra
00251168  00251170  00170000  00000000        78        d0  busy extra user_flag
00527730  00527738  00520000  00000000        40        40  busy extra
00527920  00527928  00520000  00000000        40        80  busy extra
21 leaks detected.
```

この例の表には、検出された21個のリークがすべて含まれています。

**! Heap-x**コマンドの例を次に示します。

```dbgcmd
0:011> !heap 002057b8 -x
## Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra
```

**! Heap-x-v**コマンドの例を次に示します。

```dbgcmd
1:0:011> !heap 002057b8 -x -v
## 1:Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra

Search VM for address range 002057a8 - 002057ff : 00205990 (002057d0),
```

この例では、アドレス0x00205990 のこのヒープブロックへのポインターが存在します。

**! Flt s**コマンドの例を次に示します。

```dbgcmd
0:001>!heap -flt s 0x50
```

これにより、サイズ0x50 のすべての割り当てが表示されます。

**! Flt r**コマンドの例を次に示します。

```dbgcmd
0:001>!heap -flt r 0x50 0x80
```

これにより、サイズが0x50 から0x7F までの各割り当てが表示されます。

次に、 **! heap-srch**コマンドの例を示します。

```dbgcmd
0:001> !heap -srch 77176934
    _HEAP @ 00090000
   in HEAP_ENTRY: Size : Prev Flags - UserPtr UserSize - state
        00099A48: 0018 : 0005 [01] - 00099A50 (000000B8) - (busy)
          ole32!CALLFRAME_CACHE<INTERFACE_HELPER_CLSID>::`vftable'
    _HEAP @ 00090000
   in HEAP_ENTRY: Size : Prev Flags - UserPtr UserSize - state
        00099B58: 0018 : 0005 [01] - 00099B60 (000000B8) - (busy)
          ole32!CALLFRAME_CACHE<INTERFACE_HELPER_CLSID>::`vftable'
```

次の図は、ヒープブロックの配置を示しています。

ライトページヒープブロック-割り当て済み:

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with E0 if zeroing not requested) 
    Block header (starts with 0xABCDAAAA and ends with 0xDCBAAAAA) 
```

ライトページヒープブロック--解放された:

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with F0 bytes)          
    Block header (starts with 0xABCDAAA9 and ends with 0xDCBAAA9) 
```

ページヒープブロック全体: 割り当て済み:

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (if zeroing not requested, filled   
            with C0)       
    Block header (starts with 0xABCDBBBB and ends with 0xDCBABBBB) 
```

完全なページヒープブロック--解放されています:

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (filled with F0 bytes)            
    Block header (starts with 0xABCDBBA and ends with 0xDCBABBBA) 
```

ヒープブロックまたは完全ページヒープブロックの割り当てまたは解放のスタックトレースを表示するには、ヘッダーアドレスを含む[**dt dph\_\_ブロック情報**](dt--display-type-.md)を使用し、その後、ブロックの**StackTrace**フィールドで[**dds**](dds--dps--dqs--display-words-and-symbols-.md)を使用します。
