---
title: ヒープ
description: ヒープの拡張機能ヒープ使用量の情報を表示するには、ヒープ マネージャー内のブレークポイントを制御、検出し、リークしたヒープ ブロックをヒープのブロックを検索またはページ ヒープ情報が表示されます。
ms.assetid: 70947b56-1a8c-4e78-85d0-d5df87f3150c
keywords:
- ヒープ使用量
- GFlags、ページ ヒープを有効にします。
- Windows デバッグ ヒープ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- heap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5551b7ee85e5b7cd7f01635e76a7f87bad472c87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336531"
---
# <a name="heap"></a>!heap


**! ヒープ**拡張機能のヒープ使用量の情報が表示されます、ヒープ マネージャー内のブレークポイントを制御、検出し、リークしたヒープ ブロックをヒープのブロックを検索またはページ ヒープ情報が表示されます。

この拡張機能は、セグメント ヒープと NT ヒープをサポートします。 使用! ヒープを使用するとすべてのヒープとその型を一覧表示します。

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

## <a name="span-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspansegment-and-nt-heap-parameters"></a><span id="Segment_and_NT_Heap_Parameters"></span><span id="segment_and_nt_heap_parameters"></span><span id="SEGMENT_AND_NT_HEAP_PARAMETERS"></span>セグメントと NT ヒープ パラメーター


これらのパラメーターは、セグメントと NT ヒープ機能します。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
概要情報が要求されていることを指定します。 場合*SummaryOptions*と*StatHeapAddress*を省略した場合、ヒープ、現在のプロセスに関連付けられているすべての概要情報が表示されます。

<span id="_______SummaryOptions______"></span><span id="_______summaryoptions______"></span><span id="_______SUMMARYOPTIONS______"></span> *SummaryOptions*   
次のオプションの組み合わせにすることができます。 *SummaryOptions*小文字は区別されません。 型。 ヒープの-s - でしょうか。 詳細についてはします。

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
<td align="left"><p>すべてのデータ ブロックを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong> <em>BucketSize</em></p></td>
<td align="left"><p>バケットのサイズを指定します。 既定では 1024 ビットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong> <em>DumpBlockSize</em></p></td>
<td align="left"><p>バケットのサイズを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-</strong></p></td>
<td align="left"><p>ヒープのすべてのブロックをダンプします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>各ブロックの内容を表示することを指定します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-triage__Handle___Address___"></span><span id="_______-triage__handle___address___"></span><span id="_______-TRIAGE__HANDLE___ADDRESS___"></span> **-トリアージ\[** <em>処理</em> **|** <em>アドレス</em> **\]**    
デバッガーによって自動的にプロセスのヒープ内のエラーの検索をによりします。 ヒープを処理する場合は、引数として指定して、そのヒープが調べられます。それ以外の場合、特定のアドレスが含まれているすべてのヒープを検索しが調べられる 1 つが見つかった場合します。 使用して **-トリアージ**低断片化ヒープ (LFH) の破損を検証する唯一の方法です。

<span id="_______-x_-v_"></span><span id="_______-X_-V_"></span> **-x** **** \[ **-v**\]   
原因のデバッガーが、指定したアドレスを含むヒープ ブロックを検索します。 -V を追加すると、コマンドはこのヒープ ブロックへのポインターの現在のプロセスの全体の仮想メモリ空間を検索します。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
検出するために、デバッガーのリークの原因は、ブロックをヒープします。

<span id="_______-i________Address______-h_HeapAddress______"></span><span id="_______-i________address______-h_heapaddress______"></span><span id="_______-I________ADDRESS______-H_HEAPADDRESS______"></span> **-i**  ****  *アドレス* **-h** *HeapAddress*    
指定した情報が表示されます*ヒープ*します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
検索対象のアドレスを指定します。

<span id="_______-_______"></span> **-?**    
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。 使用 **。 ヒープのでしょうか。** 汎用的なヘルプについてと **!-p - ヒープのでしょうか。** ページ ヒープ ヘルプを参照します。

## <a name="span-idddk__heap_dbgspanspan-idddk__heap_dbgspannt-heap-parameters"></a><span id="ddk__heap_dbg"></span><span id="DDK__HEAP_DBG"></span>NT ヒープ パラメーター


これらのパラメーターは、NT ヒープでのみ動作します。

<span id="_______HeapOptions______"></span><span id="_______heapoptions______"></span><span id="_______HEAPOPTIONS______"></span> *HeapOptions*   
次のオプションの組み合わせにすることができます。 *HeapOptions*値小文字は区別されます。

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
<td align="left"><p>指定されたヒープの検証にデバッガーとします。</p>
<div class="alert">
<strong>注</strong>  このオプションは低断片化 (LFH) をヒープの破損を検出しません。 使用<strong>-トリアージ</strong>代わりにします。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-</strong></p></td>
<td align="left"><p>指定されたヒープのすべての情報が表示をによりします。 サイズ、ここでは切り上げヒープ粒度にします。 (を実行している<strong>! ヒープ</strong>で、 <strong>-</strong>オプションは次の 3 つのオプションを使用して実行することに相当<strong>-h f-m</strong>、この時間がかかることができます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-h</strong></p></td>
<td align="left"><p>指定されたヒープのすべての非 LFH エントリを含めるに表示をによりします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-hl</strong></p></td>
<td align="left"><p>LFH エントリを含む、指定されたヒープのすべてのエントリを含めるにディスプレイをによりします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-f</strong></p></td>
<td align="left"><p>指定されたヒープのすべてのフリー リスト エントリを含めるにディスプレイをによりします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong></p></td>
<td align="left"><p>指定されたヒープのセグメントのすべてのエントリが表示をによりします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>指定されたヒープのタグ情報が追加表示をによりします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-T</strong></p></td>
<td align="left"><p>指定されたヒープの擬似タグ エントリを含めるに表示をによりします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-g</strong></p></td>
<td align="left"><p>グローバルのタグ情報が追加ディスプレイをによりします。 グローバルのタグは、各タグなしの割り当てに関連付けられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>指定されたヒープの概要情報が表示をによりします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-k</strong></p></td>
<td align="left"><p>(x86 ベース ターゲットのみ)各エントリに関連付けられている stack backtrace 表示をによりします。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ValidationOptions______"></span><span id="_______validationoptions______"></span><span id="_______VALIDATIONOPTIONS______"></span> *ValidationOptions*   
次のオプションのいずれかの 1 つができます。 *ValidationOptions*小文字が区別されます。

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
<td align="left"><p>検証で-得るために、指定したヒープのを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-E</strong></p></td>
<td align="left"><p>検証で-得るために、指定したヒープのを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>ヒープの指定されたヒープのチェックを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>ヒープの指定されたヒープのチェックを有効にします。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-i________Heap_Address______or_HeapAddress______"></span><span id="_______-i________heap_address______or_heapaddress______"></span><span id="_______-I________HEAP_ADDRESS______OR_HEAPADDRESS______"></span> **-i**  ****  *ヒープ*  ****  *アドレス* **または** *HeapAddress*   
指定した情報が表示されます*ヒープ*します。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
ブレークポイントが設定または削除がブロックのアドレスを指定します。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
原因のデバッガーが、ヒープ マネージャーで条件付きブレークポイントを作成します。 **-B**オプションの後に**アロケーション**、 **realloc**、または**無料**; で、ブレークポイントが有効にするかどうかを指定します割り当て、再割り当て、またはメモリを解放します。 場合*BreakAddress*はブロックのアドレスを指定するために、ブレークポイントの種類を省略できます。 場合*ヒープ*はヒープ インデックスまたはヒープのアドレスを指定するために使用、型でなければなりません、含まれるだけでなく*タグ*パラメーター。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span> *タグ*   
ヒープ内のタグ名を指定します。

<span id="_______-B______"></span><span id="_______-b______"></span> **B**   
原因のデバッガーが、ヒープ マネージャーから条件付きブレークポイントを削除します。 ブレークポイントの種類 (**アロケーション**、 **realloc**、または**無料**) を指定してで使用すると同じである必要があります、 **-b**オプション。

<span id="_______StatHeapAddress______"></span><span id="_______statheapaddress______"></span><span id="_______STATHEAPADDRESS______"></span> *StatHeapAddress*   
ヒープのアドレスを指定します。 これは、0 または省略すると、ヒープ、現在のプロセスに関連付けられているすべてが表示されます。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
ページ ヒープの情報が要求されていることを指定します。 なく、使用される場合*PageHeapOptions*、すべてのページがヒープが表示されます。

<span id="_______PageHeapOptions______"></span><span id="_______pageheapoptions______"></span><span id="_______PAGEHEAPOPTIONS______"></span> *PageHeapOptions*   
次のオプションのいずれかの 1 つができます。 *PageHeapOptions*小文字が区別されます。 オプションが指定されていない場合はすべての可能なページ ヒープ ハンドルが表示されます。

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
<td align="left"><p><strong>-h</strong> <em>処理</em></p></td>
<td align="left"><p>デバッガーがハンドルを持つページ ヒープに関する詳細情報を表示<em>処理</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-</strong> <em>アドレス</em></p></td>
<td align="left"><p>デバッガーが持つブロックが含まれるページ ヒープを見つける<em>アドレス</em>します。 このアドレスは、ページ ヒープの場合、そのオフセット、ブロック内の一部かどうかと、ブロックが割り当てられているまたは解放されたかどうか、このアドレスが完全ページ ヒープ ブロックに関連付ける方法の完全な詳細情報が含められます。 使用可能な場合、スタック トレースが含まれます。 このオプションを使用する場合は、ヒープ割り当ての粒度の倍数単位のサイズが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong>[<strong>c</strong>|<strong>s</strong>] [<em>Traces</em>]</p></td>
<td align="left"><p>原因のデバッガーがヒープの負荷の高いユーザーの収集されたトレースを表示します。 <em>トレース</em>; を表示するトレースの数を指定します。 既定値は 4 つです。 指定した数よりも多くのトレースがある場合は、最も古いトレースが表示されます。 場合<strong>-t</strong>または<strong>-tc</strong>が使用すると、トレースが数の使用量により並べ替えられました。 場合<strong>ts</strong>が使用すると、トレースはサイズに基づいて並べ替えられています。 (、 <strong>-Tc</strong>と<strong>ts</strong>オプションは Windows XP でのみサポートされて、 <strong>-t</strong>オプションは、Windows XP および Windows の以前のバージョンでのみサポートされます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-fi</strong> [<em>トレース</em>]</p></td>
<td align="left"><p>原因のデバッガーが最新のフォールト インジェクション トレースを表示します。 <em>トレース</em>数量を表示する; 指定、既定値は 4 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-すべて</strong></p></td>
<td align="left"><p>原因のデバッガーがヒープにすべてのページに関する詳細情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-?</strong></p></td>
<td align="left"><p>ヒープ ブロックのダイアグラムを含むページ ヒープのヘルプを表示するデバッガーをによりします。 (これらの図もでわかるように、次の「解説」です。)</p></td>
</tr>
</tbody>
</table>

 

いずれかを使用する前に **。 ヒープの-p**拡張機能のコマンドを、ターゲット プロセスのページ ヒープを有効にする必要があります。 次の「解説」で詳細を参照してください。

<span id="_______-srch______"></span><span id="_______-SRCH______"></span> **-srch**   
指定したパターンのすべてのヒープをスキャンします。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
検索対象のパターンを指定します。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
次のオプションのいずれかの 1 つができます。 これには、パターンのサイズを指定します。 '-' が必要です。

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
<td align="left"><p>パターンのサイズは 1 バイトです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>パターンは、サイズの 1 つの単語です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>パターンは、1 つの DWORD のサイズです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-q</strong></p></td>
<td align="left"><p>パターンは、1 つの QWORD サイズです。</p></td>
</tr>
</tbody>
</table>

 

指定しないと、上記の場合は、マシン ポインターと同じサイズであるパターンが使用されます。

<span id="_______-flt______"></span><span id="_______-FLT______"></span> **-flt**   
指定したサイズまたはサイズの範囲でヒープのみが表示を制限します。

<span id="_______FilterOptions______"></span><span id="_______filteroptions______"></span><span id="_______FILTEROPTIONS______"></span> *FilterOptions*   
次のオプションのいずれかの 1 つができます。 *FilterOptions*小文字が区別されます。

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
<td align="left"><p>指定したサイズのヒープのみが表示を制限します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> <em>SizeMin</em> <em>SizeMax</em></p></td>
<td align="left"><p>指定したサイズの範囲内でヒープのみが表示を制限します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-stat______"></span><span id="_______-STAT______"></span> **-stat**   
指定されたヒープの使用状況の統計を表示します。

<span id="_______-h________Handle______"></span><span id="_______-h________handle______"></span><span id="_______-H________HANDLE______"></span> **-h** *処理*   
使用状況の統計、ヒープにのみ発生*処理*に表示されます。 場合*処理*が 0 または省略すると、すべてのヒープ使用量の統計が表示されます。

<span id="_______-grp________GroupBy______"></span><span id="_______-grp________groupby______"></span><span id="_______-GRP________GROUPBY______"></span> **-grp** **** *GroupBy*   
指定された表示を並べ替えます*GroupBy*します。 オプション*GroupBy*は次の表にあります。

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
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>アロケーション サイズに従って使用状況の統計を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>ブロック数に従って使用状況の統計を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>各割り当ての合計サイズに応じて使用状況の統計を表示します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______MaxDisplay______"></span><span id="_______maxdisplay______"></span><span id="_______MAXDISPLAY______"></span> *MaxDisplay*   
出力のみを制限します*MaxDisplay*行の数。

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
Ext.dll Exts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ヒープの詳細については、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

この拡張機能のコマンドは、さまざまなタスクの実行に使用できます。

標準 **! ヒープ**コマンドを使用して、現在のプロセスのヒープの情報を表示します。 (ユーザー モード プロセスに対してのみこの使用する必要があります。 [ **! プール**](-pool.md)システム プロセスの拡張機能のコマンドを使用する必要があります)。

**! ヒープ-b**と **!-b をヒープ**コマンドを使用して作成し、ヒープ マネージャーで条件付きブレークポイントを削除します。

**。 ヒープの-l**コマンドがリークしたヒープ ブロックを検出します。 プロセスのアドレス空間内で参照されていないヒープからのすべての使用中ブロックを検出するために、ガベージ コレクターのアルゴリズムを使用します。 大きなアプリケーションでは、完了に数分をかかります。 このコマンドは、Windows XP および Windows の以降のバージョンで使用できるだけです。

**! ヒープ-x**コマンド、特定のアドレスを含むヒープ ブロックを検索します。 場合、 **-v**オプションを使用すると、このコマンドはこのヒープ ブロックへのポインターの現在のプロセスの全体の仮想メモリ空間を検索してさらにします。 このコマンドは、Windows XP および Windows の以降のバージョンで使用できるだけです。

**。 ヒープの-p**コマンドは、さまざまな形式のページ ヒープの情報を表示します。 使用する前に **。 ヒープの-p**、ターゲット プロセスのページ ヒープを有効にする必要があります。 これは、グローバル フラグ (gflags.exe) ユーティリティを使用します。 これを行うには、ユーティリティを起動し、ターゲット アプリケーションの名前を入力、**イメージ ファイル名**テキスト ボックスで、 **Image File Options**と**ページ ヒープを有効にする**、 をクリック**適用**します。 」と入力してコマンド プロンプト ウィンドウからグローバル フラグ ユーティリティを起動する代わりに、 **gflags/i** *xxx.exe* **+ hpa**ここで、 *xxx.exe*対象アプリケーションの名前を指定します。

**!-P t をヒープ\[c | s\]** コマンドは、Windows XP 以外はサポートされていません。 使用して、 [UMDH](umdh.md)のような結果を得るためのデバッガー パッケージで提供されるツールです。

**! ヒープ - srch**コマンドは、特定の指定したパターンが含まれているこれらのヒープ エントリを表示します。

**! ヒープ - flt**コマンドにのみ、指定したサイズの割り当てをヒープに制限します。

**! ヒープ - stat**コマンドは、ヒープの使用状況の統計を表示します。

標準の例を次に示します **! ヒープ**コマンド。

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

次の例に示します、 **。 ヒープの-l**コマンド。

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

この例では、テーブルには、検出されたすべての 21 リークが含まれています。

次の例に示します、 **! ヒープ-x**コマンド。

```dbgcmd
0:011> !heap 002057b8 -x
## Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra
```

次の例に示します、 **! ヒープ-x v**コマンド。

```dbgcmd
1:0:011> !heap 002057b8 -x -v
## 1:Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra

Search VM for address range 002057a8 - 002057ff : 00205990 (002057d0),
```

この例では、アドレス 0x00205990 でこのヒープ ブロックへのポインターです。

次の例に示します、 **! ヒープ - flt s**コマンド。

```dbgcmd
0:001>!heap -flt s 0x50
```

これは、すべて 0x50 のサイズの割り当てに表示されます。

次の例に示します、 **! ヒープ - flt r**コマンド。

```dbgcmd
0:001>!heap -flt r 0x50 0x80
```

各割り当てのサイズは 0x50 とから 0x7f までの間が表示されます。

次の例に示します、 **! ヒープ - srch**コマンド。

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

次の図は、ヒープ ブロックの並べ替え方法を示します。

割り当てられた - 簡易ページ ヒープ ブロック:

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with E0 if zeroing not requested) 
    Block header (starts with 0xABCDAAAA and ends with 0xDCBAAAAA) 
```

簡易ページ ヒープ ブロック--解放:

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with F0 bytes)          
    Block header (starts with 0xABCDAAA9 and ends with 0xDCBAAA9) 
```

割り当てられた--完全ページ ヒープ ブロック:

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

完全ページ ヒープ ブロック--解放:

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (filled with F0 bytes)            
    Block header (starts with 0xABCDBBA and ends with 0xDCBABBBA) 
```

割り当てのスタック トレースまたはヒープ ブロックまたは完全ページ ヒープ ブロックの解放を表示する[ **dt DPH\_ブロック\_情報**](dt--display-type-.md) 続けて、ヘッダーのアドレスを使用[**dds** ](dds--dps--dqs--display-words-and-symbols-.md)ブロックの**StackTrace**フィールド。

 

 





