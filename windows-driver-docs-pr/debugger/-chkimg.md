---
title: chkimg
description: Chkimg 拡張機能は、シンボル ストアまたはその他のファイルのリポジトリ上のコピーと比較して、実行可能ファイルのイメージの破損を検出します。
ms.assetid: 8079676c-1138-4c60-95df-62fd270fee62
keywords:
- 実行可能ファイルとパス、破損
- Windows デバッグ chkimg
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chkimg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae67307c931ac6a412275351e5366107daa5ea36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575041"
---
# <a name="chkimg"></a>!chkimg


**! Chkimg**拡張機能は、シンボル ストアまたはその他のファイルのリポジトリ上のコピーと比較して実行可能ファイルのイメージの破損を検出します。

```dbgsyntax
!chkimg [Options] [-mmw LogFile LogOptions] [Module]
```

## <a name="span-idddkchkimgdbgspanspan-idddkchkimgdbgspanparameters"></a><span id="ddk__chkimg_dbg"></span><span id="DDK__CHKIMG_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせには:

<span id="-p_SearchPath_"></span><span id="-p_searchpath_"></span><span id="-P_SEARCHPATH_"></span>**-p** **** *検索パス*   
再帰的に検索*SearchPath*シンボル サーバーにアクセスする前にファイル。

<span id="-f"></span><span id="-F"></span>**-f**  
イメージのエラーを修正します。 スキャンがメモリ内のシンボル ストア上のファイルとイメージの違いを検出する、シンボル ストア上のファイルの内容は、イメージ上でコピーされます。 ライブ デバッグを実行する場合は、実行する前にダンプ ファイルを作成することができます、 **! chkimg f**拡張機能。

<span id="-nar"></span><span id="-NAR"></span>**-nar**  
シンボル サーバー上のファイルのマップされたイメージが移動されないようにします。 ファイルのコピーがシンボル サーバー上にあり、メモリにマップした場合、既定 **! chkimg**シンボル サーバー上のファイルのイメージを移動します。 ただし、使用する場合、 **- nar**オプション、サーバーからファイルのイメージは移動されません。

メモリ (スキャンされているもの) にある実行可能イメージを移動すると、デバッガーは常に読み込まれるイメージを再配置するためです。

このスイッチは、オペレーティング システムが既に元のイメージを移動する場合にのみ役立ちます。 イメージが移動されていない場合 **! chkimg**デバッガーは、イメージを移動します。 このスイッチの使用はまれです。

<span id="-ss_SectionName_"></span><span id="-ss_sectionname_"></span><span id="-SS_SECTIONNAME_"></span>**-ss** **** *SectionName*   
これらのセクションでは、名前に文字列を含むにスキャン制限*SectionName*します。 スキャンは、名前持つにはには、この文字列が含まれています。 非破棄セクションが含まれます。 *SectionName*は大文字小文字を区別し、8 文字を超えることはできません。

<span id="-as"></span><span id="-AS"></span>**-として**  
破棄できるセクション以外のすべてのセクションを含めるスキャンをによりします。 既定では、(を使用しない場合 **-として**または **-ss**) が書き込み可能のセクションで、実行可能ファイルではないのセクションでは、セクションでは、名前に「ページ」を持つおよび破棄できるのセクションでは、スキャンをスキップします。

<span id="-r_StartAddress_EndAddress__"></span><span id="-r_startaddress_endaddress__"></span><span id="-R_STARTADDRESS_ENDADDRESS__"></span>**-r** **** *StartAddress* **** *EndAddress*   
始まるメモリ範囲をスキャン制限*StartAddress*で終わります*EndAddress*します。 この範囲内では、スキャンする通常のあるすべてのセクションがスキャンされます。 セクションがこの範囲を部分的に重なっている場合は、この範囲と重複するセクションの部分のみがスキャンされます。 場合でも、使用することも、スキャンがこの範囲に制限されていますが、 **-として**または **-ss**スイッチします。

<span id="-nospec"></span><span id="-NOSPEC"></span>**-nospec**  
含める Hal.dll と Ntoskrnl.exe の予約済みのセクションでは、スキャンをによりします。 既定では、 **! chkimg**これらのファイルの特定の部分をチェックしません。

<span id="-noplock"></span><span id="-NOPLOCK"></span>**-noplock**  
不一致 0x90 のバイト値のことで領域を表示します (、 **nop**命令) および 0xF0 のバイト値 (、**ロック**命令)。 既定では、これらの不一致は表示されません。

<span id="-np"></span><span id="-NP"></span>**-np**  
エラーの原因は、認識されるようにする手順を修正しました。

<span id="-d"></span><span id="-D"></span>**-d**  
スキャンの実行中に一致しないすべての領域の概要が表示されます。 この概要のテキストの詳細については、「解説」を参照してください。

<span id="-db"></span><span id="-DB"></span>**-db**  
次のような形式で一致しない部分が表示されます、 [ **db デバッガー コマンド**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)します。 そのため、各表示行の行で、最初のバイトのアドレスを表示するは、最大 16 の 16 進のバイト値によって続きます。 バイト値のすぐ後で、対応する ASCII 値。 キャリッジ リターンとライン フィードなどのすべての印刷できない文字がピリオド (.) として表示されます。 不一致のバイトがアスタリスクによってマークされている (\*)。

<span id="-lo_lines"></span><span id="-LO_LINES"></span>**-lo** **** *行*  
制限出力の数の行を **-d**または**db**行の行の数を表示します。

<span id="-v"></span><span id="-V"></span>**-v**  
詳細な情報を表示します。

<span id="_______-mmw______"></span><span id="_______-MMW______"></span> **-mmw**   
ログ ファイルを作成しの動作を記録 **! chkimg**このファイルにします。 ログ ファイルの各行は、1 つの不一致を表します。

<span id="_______LogFile______"></span><span id="_______logfile______"></span><span id="_______LOGFILE______"></span> *LogFile*   
ログ ファイルの完全なパスを指定します。 相対パスを指定する場合は、現在のパスの相対パスです。

<span id="_______LogOptions______"></span><span id="_______logoptions______"></span><span id="_______LOGOPTIONS______"></span> *LogOptions*   
ログ ファイルの内容を指定します。 *LogOptions*はさまざまな文字を連結したもので構成される文字列です。 ログ ファイルの各行には、コンマで区切られた複数の列が含まれています。 これらの列に文字が表示される順序で、次のオプションの文字を指定する項目を含める、 *LogOptions*文字列。 次のオプションは、複数回含めることができます。 少なくとも 1 つのオプションを含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ログ オプション</th>
<th align="left">ログ ファイルに含まれる情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>v</p></td>
<td align="left"><p>不一致の仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>モジュール内の不一致のオフセット (相対アドレス)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>s</p></td>
<td align="left"><p>不一致のアドレスに対応するシンボル</p></td>
</tr>
<tr class="even">
<td align="left"><p>S</p></td>
<td align="left"><p>不一致を格納するセクションの名前</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>正しい値が一致しない場所で必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>不適切な値が一致しない場所にだった</p></td>
</tr>
</tbody>
</table>

 

*LogOptions*か、次のオプションのいずれかにも含めることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ログ オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>O</p></td>
<td align="left"><p>場合、名前を持つファイル<em>LogFile</em>が既に存在する既存のファイルが上書きされます。 既定では、デバッガーは、既存のファイルの末尾に新しい情報を追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>t<em>文字列</em></p></td>
<td align="left"><p>ログ ファイルに、余分な列を追加します。 このコラムでは、各エントリが含まれる<em>文字列</em>します。 <strong>T</strong><em>文字列</em>オプションは、既存のログ ファイルに新しい情報を追加して、古いから新しいレコードを区別する必要がある場合に便利です。 間にスペースを追加することはできません<strong>t</strong>と<em>文字列</em>します。 使用する場合、 <strong>t</strong>は<em>文字列</em>オプション、する必要がありますで最後のオプション<em>LogOptions</em>ため、<em>文字列</em>に含めるすべての実行は、次の領域の前に存在する文字。</p></td>
</tr>
</tbody>
</table>

 

たとえば場合、 *LogOptions*は**rSewo**、ログ ファイルの各行が一致しない場所とその場所での予測と実際の値の相対アドレスとセクション名が含まれています。 このオプションによって、前のファイルを上書きします。 使用することができます、 **- mmw**スイッチを複数回さまざまなオプションがあるいくつかのログ ファイルを作成する場合。 同時に、最大 10 個のログ ファイルを作成できます。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
チェックするモジュールを指定します。 *モジュール*モジュール、モジュールの開始アドレスまたはモジュールに含まれている任意のアドレスの名前を指定できます。 省略した場合*モジュール*デバッガーは現在の命令ポインターを格納しているモジュールを使用します。

<span></span>  

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

 

<a name="remarks"></a>コメント
-------

使用すると **! chkimg**、シンボル ストアに存在するファイルのコピーをメモリ内で実行可能ファイルのイメージと比較します。

セクションでは、破棄できる、書き込み可能である、実行可能ファイルではない、名前に「ページ」があるまたは INITKDBG はを除き、ファイルのすべてのセクションが比較されます。 使用してこの動作のことができますを変更することができます、 **-ss**、 **-として**、または **-r**スイッチ。

**! chkimg**イメージ エラー、次の例外として、イメージとファイル間に不一致が表示されます。

-   インポート アドレス テーブル (IAT) によって占有されるアドレスはチェックされません。

-   これらのセクションが読み込まれるときに、特定の変更が行われるため、特定 Hal.dll と Ntoskrnl.exe で特定のアドレスはチェックされません。 これらのアドレスを確認するには、 **- nospec**オプション。

-   0x90 バイトの値は、ファイル内に存在し、値は 0xf0 です. は、イメージの (またはその逆) に対応するバイトに存在する場合は、このような状況は、一致と見なされます。 通常、シンボル サーバーは、両方のプロセッサが存在するバイナリの 1 つのバージョン、およびマルチプロセッサのバージョンを保持します。 X86 ベースのプロセッサでは、上、**ロック**命令は 0xF0、この命令に対応する、 **nop**ユニプロセッサ バージョン (0x90) 命令。 場合 **! chkimg**が一致しないと、このペアを表示するには、設定、 **- noplock**オプション。

**注**  を使用する場合、 **-f**イメージの不一致を修正する選択肢 **! chkimg**のエラーと見なされる場合の不一致のみを修正します。 たとえば、 **! chkimg** 、0x90 バイトに変わらない、0xF0 バイトを含めない限り、 **- noplock**します。

 

含めた場合、 **-d**オプション、 **! chkimg**スキャンの実行中に一致しないすべての領域の概要を表示します。 各不一致は、2 つの行に表示されます。 最初の行には、範囲、範囲の末尾の範囲では、シンボル名および直近のエラー (かっこ内) からのバイト数の範囲の開始に対応するオフセット、サイズの開始が含まれています。 2 行目では、角かっこで囲まれたし、画像の 16 進のバイト値が必要ですが、コロン、および実際に発生した 16 進のバイト値が含まれています。 範囲が 8 バイトより長い場合、コロンの前に、コロンの後に最初の 8 バイトだけが表示されます。 次の例では、このような状況を示します。

```dbgcmd
be000015-be000016  2 bytes - win32k!VeryUsefulFunction+15 (0x8)
     [ 85 dd:95 23 ]
```

場合によっては、ドライバーは、フック、リダイレクト、またはその他のメソッドを使用して、Microsoft Windows カーネルの一部を変更します。 不要になったスタック上にあるドライバーも、カーネルの一部変更可能性があります。 使用することができます、 **! chkimg**ドライバーによって Windows カーネル (または他のイメージ) のどの部分が変更されていると、部分をどのように変更するだけを確認するファイル比較ツールとして拡張機能。 この比較は、完全なダンプ ファイルに最も効果的です。

使用することもできます **! chkimg**と共に、 [ **! の\_各\_モジュール**](-for-each-module.md)拡張機能を読み込まれている各モジュールのイメージを確認します。 次の例では、このような状況を示します。

```dbgcmd
!for_each_module !chkimg @#ModuleName 
```

たとえば、バグ チェックが発生しを使用して開始したと[ **! 分析**](-analyze.md)します。

```dbgcmd
kd> !analyze 
....
BugCheck 1000008E, {c0000005, bf920e48, baf75b38, 0}
Probably caused by : memory_corruption
CHKIMG_EXTENSION: !chkimg !win32k
....
```

この例で、 [ **! 分析**](-analyze.md)出力は、そのメモリを提案の破損が発生し、CHKIMG が含まれています\_Win32k.sys が破損しているモジュールにあることを示す行を拡張します。 (場合でも、この行が存在しない可能性があるスタックの一番上のモジュールで破損している可能性。)使用して開始 **! chkimg**スイッチを指定せず、次の例として示します。

```dbgcmd
kd> !chkimg win32k
Number of different bytes for win32k: 31
```

メモリの破損が実際には、次の例です。 使用 **! chkimg-d** Win32k モジュールは、エラーのすべてを表示します。

```dbgcmd
kd> !chkimg win32k -d
    bf920e40-bf920e46  7 bytes - win32k!HFDBASIS32::vSteadyState+1f
        [ 78 08 d3 78 0c c2 04:00 00 00 00 00 01 00 ]
    bf920e48-bf920e5f  24 bytes - win32k!HFDBASIS32::vHalveStepSize (+0x08)
        [ 8b 51 0c 8b 41 08 56 8b:00 00 00 00 00 00 00 00 ]
Number of different bytes for win32k: 31
```

表示されている 2 番目のセクションの破損したイメージを逆アセンブルするときは、次の出力が表示される場合があります。

```dbgcmd
kd> u  win32k!HFDBASIS32::vHalveStepSize
win32k!HFDBASIS32::vHalveStepSize:
bf920e48 0000             add     [eax],al
bf920e4a 0000             add     [eax],al
bf920e4c 0000             add     [eax],al
bf920e4e 0000             add     [eax],al
bf920e50 7808            js win32k!HFDBASIS32::vHalveStepSize+0x12 (bf920e5a)
bf920e52 d3780c           sar     dword ptr [eax+0xc],cl
bf920e55 c20400           ret     0x4
bf920e58 8b510c           mov     edx,[ecx+0xc]
```

使用して、 **! chkimg f**メモリ破損を修復します。

```dbgcmd
kd> !chkimg win32k -f
Warning: Any detected errors will be fixed to what we expect!
Number of different bytes for win32k: 31 (fixed)
```

修正済みのビューを逆アセンブルを行った変更内容を確認できます。

```dbgcmd
kd> u  win32k!HFDBASIS32::vHalveStepSize
win32k!HFDBASIS32::vHalveStepSize:
bf920e48 8b510c           mov     edx,[ecx+0xc]
bf920e4b 8b4108           mov     eax,[ecx+0x8]
bf920e4e 56               push    esi
bf920e4f 8b7104           mov     esi,[ecx+0x4]
bf920e52 03c2             add     eax,edx
bf920e54 c1f803           sar     eax,0x3
bf920e57 2bf0             sub     esi,eax
bf920e59 d1fe             sar     esi,1
```

 

 





