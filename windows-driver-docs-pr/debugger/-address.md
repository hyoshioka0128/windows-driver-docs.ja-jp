---
title: address
description: アドレスの拡張機能には、ターゲット プロセスまたは対象のコンピューターで使用されるメモリに関する情報が表示されます。
ms.assetid: 9bbde680-8523-4db2-bb7e-fdacdaf1aa89
keywords:
- Windows デバッグ アドレス
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- address
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7763b9c07c2d2a34e9a3c1f3838a3266a0743c6e
ms.sourcegitcommit: bb4f9c8dab2f4cb7a57ebd30457f427d909c928f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2019
ms.locfileid: "58624779"
---
# <a name="address"></a>!address


**! アドレス**拡張機能がターゲット プロセスまたは対象のコンピューターで使用されるメモリに関する情報を表示します。

ユーザー モード

```dbgcmd
!address Address
!address -summary 
!address [-f:F1,F2,...] {[-o:{csv | tsv | 1}] | [-c:"Command"]}
!address -? | -help
```

カーネル モード

```dbgcmd
!address Address 
!address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
アドレス空間を含むの領域のみを表示*アドレス*します。

<span id="_______-summary______"></span><span id="_______-SUMMARY______"></span> **-summary**   
概要情報のみが表示されます。

<span id="_______-f_F1__F2__..."></span><span id="_______-f_f1__f2__..."></span><span id="_______-F_F1__F2__..."></span> **-f**:*F1*、 *F2*、.  
フィルターが指定されている領域のみを表示します。 *F1*、 *F2*など。

次のフィルター値は、ターゲット プロセスを使用しているこれらの方法でメモリ領域を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値をフィルター処理します。</th>
<th align="left">メモリ領域が表示されます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VAR</p></td>
<td align="left"><p>使用中のリージョン。 これらのリージョンには、仮想の割り当てのすべてのブロック、SBH ヒープ、メモリからカスタム アロケーターは、ないその他の分類に分類されるアドレス空間の他のすべての領域などがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Free</p></td>
<td align="left"><p>空きメモリ。 これには、予約されていないすべてのメモリが含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>イメージ</p></td>
<td align="left"><p>実行可能イメージの一部であるファイルに割り当てられるメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>スタック</p></td>
<td align="left"><p>スレッドのスタックに使用されるメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>teb</p></td>
<td align="left"><p>スレッド環境ブロック (TEBs) に使用されるメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peb</p></td>
<td align="left"><p>プロセスの環境ブロック (PEB) に使用されるメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ヒープ</p></td>
<td align="left"><p>メモリがヒープのために使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Pageheap によって</p></td>
<td align="left"><p>メモリ領域は、完全ページ ヒープのために使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CSR</p></td>
<td align="left"><p>CSR は、メモリを共有します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Actx</p></td>
<td align="left"><p>アクティブ化コンテキストのデータに使用されるメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NLS</p></td>
<td align="left"><p>各国語サポート (NLS) のテーブルに対して使用されるメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルマップ</p></td>
<td align="left"><p>メモリ マップト ファイルに使用されるメモリ。 このフィルターは、ライブ デバッグ中にのみ適用できます。</p></td>
</tr>
</tbody>
</table>

 

次のフィルター値は、メモリの種類によってメモリ領域を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値をフィルター処理します。</th>
<th align="left">メモリ領域が表示されます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MEM_IMAGE</p></td>
<td align="left"><p>実行可能イメージの一部であるファイルに割り当てられるメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEM_MAPPED</p></td>
<td align="left"><p>実行可能イメージの一部でないファイルに割り当てられるメモリ。 これには、ページング ファイルに割り当てられるメモリが含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_PRIVATE</p></td>
<td align="left"><p>プライベート メモリ。 他のプロセスでは、このメモリは共有されませんし、任意のファイルにはマップされていません。</p></td>
</tr>
</tbody>
</table>

 

次のフィルター値は、メモリの状態では、メモリ領域を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値をフィルター処理します。</th>
<th align="left">メモリ領域が表示されます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MEM_COMMIT</p></td>
<td align="left"><p>コミットされたメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEM_FREE</p></td>
<td align="left"><p>空きメモリ。 これには、予約されていないすべてのメモリが含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_RESERVE</p></td>
<td align="left"><p>予約済みのメモリ。</p></td>
</tr>
</tbody>
</table>

 

次のフィルター値は、メモリに適用される保護によってメモリ領域を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値をフィルター処理します。</th>
<th align="left">メモリ領域が表示されます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>です</p></td>
<td align="left"><p>アクセスできないメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_READONLY</p></td>
<td align="left"><p>読み取り可能ながいない書き込み可能でない実行可能ファイルのメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_READWRITE</p></td>
<td align="left"><p>読み取り可能な書き込み可能なが実行不可能メモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_WRITECOPY</p></td>
<td align="left"><p>コピー オン ライト動作のあるメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE</p></td>
<td align="left"><p>つまり、実行可能ファイルが読み取り不可能といない書き込み可能なメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_READ</p></td>
<td align="left"><p>実行可能ファイルと読み取り可能ながいない書き込み可能なメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE_READWRITE</p></td>
<td align="left"><p>実行可能ファイル、読み取りおよび書き込み可能なメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_WRITECOPY</p></td>
<td align="left"><p>実行可能ファイルはコピー オン ライト動作があるメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_GUARD</p></td>
<td align="left"><p>ガード ページとして機能するメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_NOCACHE</p></td>
<td align="left"><p>キャッシュされていないメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_WRITECOMBINE</p></td>
<td align="left"><p>有効になっている結合の書き込みアクセス権を持つメモリ。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-o__csv___tsv___1_"></span><span id="_______-O__CSV___TSV___1_"></span> **-o:**{**csv** | **tsv** | **1**}  
次のオプションのいずれか 1 つの出力が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">出力の形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>csv</p></td>
<td align="left"><p>コンマ区切り値として出力が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>tsv</p></td>
<td align="left"><p>タブ区切りの値として出力が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>ベア形式で出力が表示されます。 この形式の場合にも動作<strong>! アドレス</strong>への入力として提供される <strong><a href="-foreach.md" data-raw-source="[.foreach](-foreach.md)">.foreach</a></strong>します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-c__Command_"></span><span id="_______-c__command_"></span><span id="_______-C__COMMAND_"></span> **-c**:"*コマンド*"  
各メモリ領域のカスタム コマンドを実行します。 コマンドの出力フィールドを表す、次のプレース ホルダーを使用することができます、 **! アドレス**拡張機能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[プレースホルダ]</th>
<th align="left">出力フィールド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%1</p></td>
<td align="left"><p>ベース アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>終了アドレスは + 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>領域のサイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>型</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%5</p></td>
<td align="left"><p>状態</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>保護</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>使用方法</p></td>
</tr>
</tbody>
</table>

 

たとえば、`!address -f:Heap -c:".echo %1 %3 %5"`ベース アドレス、サイズ、および型の場合は、各メモリ領域の状態を表示します。**ヒープ**します。

バック スラッシュのコマンドは、目の引用符の前が必要 (\\")。 たとえば、!-f に対処: ヒープの c:"s-a %1 %2 \\"パッド\\""型の場合は、各メモリ領域を検索**ヒープ**文字列「埋め込み」。

セミコロンで区切られた複数のコマンドはサポートされていません。

<span id="_______-_______"></span> **-?**   
この拡張機能の最小限のヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリの表示と検索する方法の詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。 メモリのプロパティを表示する追加の拡張機能を参照してください。 [ **! vm** ](-vm.md) (カーネル モード) と[ **! vprot** ](-vprot.md) (ユーザー モード)。

<a name="remarks"></a>コメント
-------

任意のパラメーターを指定せず、 **! アドレス**拡張機能は、アドレス空間全体に関する情報を表示します。 **! アドレス - 概要**コマンドは、概要のみを表示します。

この拡張機能が使用する場合でも、カーネル メモリのみを検索カーネル モードで[ **.process (プロセス コンテキストの設定)** ](-process--set-process-context-.md)特定のプロセス仮想アドレス空間を指定します。 ユーザー モードで、 **! アドレス**拡張機能は、常にターゲット プロセスを所有するメモリを指します。

ユーザー モードで **! アドレス***アドレス*に指定されたアドレスが属しているリージョンの特性を示しています。 パラメーターを指定せず **! アドレス**メモリ領域のすべての特性を示しています。 これらの特性には、メモリ使用量、メモリの種類、メモリの状態、およびメモリ保護が含まれます。 この情報の意味の詳細については、以前のテーブルの説明を参照してください、 **-f**パラメーター。

次の例では **! アドレス**kernel32.dll にマップされているメモリの領域に関する情報を取得します。

```console
0:000> !address 75831234
Usage:                  Image
Base Address:           75831000
End Address:            758f6000
Region Size:            000c5000
Type:                   01000000MEM_IMAGE
State:                  00001000MEM_COMMIT
Protect:                00000020PAGE_EXECUTE_READ
More info:              lmv m kernel32
More info:              !lmi kernel32
More info:              ln 0x75831234
```

この例では、*アドレス*0x75831234 の値。 このアドレスが、アドレス 0x75831000 で始まり、0x758f6000 アドレスで終了しているメモリ領域が表示されます。 使用状況は、リージョンが**イメージ**、型**メモリ最適化\_イメージ**、状態**MEM\_コミット**、および保護**ページ\_実行\_読み取り**します。 (これらの値の意味の詳細については、以前のテーブルを参照してください)。表示には、このメモリ アドレスに関する詳細情報を使用できるその他の 3 つのデバッガー コマンドも一覧表示されます。

アドレスを開始することに関する情報を決定しようとすると、使用状況情報は頻繁に最も重要な場合。 使用状況を確認した後は、詳細については、このメモリは追加の拡張機能を使用できます。 たとえば、次の使用方法は、**ヒープ**、使用することができます、 [ **! ヒープ**](-heap.md)拡張機能の詳細は。

次の例では、 [ **s (メモリの検索)** ](s--search-memory-.md)型の場合は、各メモリ領域を検索するコマンド**イメージ**ワイド文字の文字列「に注意してください」です。

```console
!address /f:Image /c:"s -u %1 %2 \"Note\""

*** Executing: s -u 0xab0000 0xab1000 "Note"
*** Executing: s -u 0xab1000 0xabc000 "Note"
00ab2936  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
00ab2f86  004e 006f 0074 0065 0070 0061 0064 005c  N.o.t.e.p.a.d.\.
00ab32e4  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
*** Executing: s -u 0xabc000 0xabd000 "Note"
. . .
```

カーネル モードの出力で **! アドレス**ユーザー モードの出力に似ていますが、以下の情報が含まれます。 次の例では、カーネル モードの出力を示します。

```console
kd> !address
  804de000 - 00235000                           
 Usage       KernelSpaceUsageImage
          ImageName   ntoskrnl.exe

  80c00000 - 001e1000
          Usage       KernelSpaceUsagePFNDatabase

....

  f85b0000 - 00004000
          Usage       KernelSpaceUsageKernelStack
          KernelStack 817b4da0 : 324.368

 f880d000 - 073d3000
          Usage       KernelSpaceUsageNonPagedPoolExpansion
```

"Usage"の意味では、ユーザー モードと同じです。 "ImageName"では、このアドレスに関連付けられているモジュールを示します。 "KernelStack"には、このスレッドの ETHREAD ブロック (0x817B4DA0)、プロセス ID (0x324)、およびスレッド ID (0x368) のアドレスが表示されます。

 

 





