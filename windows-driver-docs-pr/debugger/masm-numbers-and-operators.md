---
title: MASM の数値と演算子
description: MASM の数値と演算子
ms.assetid: 9aeb3ef2-d83a-4f99-9a55-4bbd8a7e11b5
keywords:
- MASM 式の構文の式
- 数値式 (MASM)
- 数値の MASM 式
- MASM の式、演算子
- 演算子 (MASM)
- (MASM プレフィックス)
- 二項演算子
- シフト演算子
- 単項演算子
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9890f3cae44d4c232876eb0cb4a498d400974e32
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464162"
---
# <a name="masm-numbers-and-operators"></a>MASM の数値と演算子


## <span id="ddk_masm_numbers_and_operators_dbg"></span><span id="DDK_MASM_NUMBERS_AND_OPERATORS_DBG"></span>


前の Windows のツールをデバッグ パッケージのバージョン 4.0、に、CDB、NTSD、KD、および WinDbg Microsoft マクロ アセンブラー (MASM) 式の構文のみを使用します。

### <a name="span-idnumbersinmasmexpressionsspanspan-idnumbersinmasmexpressionsspannumbers-in-masm-expressions"></a><span id="numbers_in_masm_expressions"></span><span id="NUMBERS_IN_MASM_EXPRESSIONS"></span>MASM の式内の番号

数値は、基本の 16、10、8、または 2 での MASM 式を格納できます。

使用して、 [ **n (設定数の基本)** ](n--set-number-base-.md)を 16、10、または 8 既定の基数を設定するコマンド。 すべてのプレフィックスのない数値は、このベースし解釈されます。 既定の基数を指定して上書きできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。

追加することで、16 進数を指定することも、 **h**番号の後です。 番号内の大文字または小文字の文字を使用することができます。 たとえば、"0x4AB3"、"0X4aB3"、"4AB3h"、"4ab3h"および"4aB3H"は同じ意味を持ちます。

式でプレフィックスの後に数字を追加しない場合、番号は 0 として読み取られます。 そのため、プレフィックスとそれに続く 0、およびプレフィックスのみ、0 として 0 を記述できます。 たとえば、16 進数、「0」、"0x0"および"0 x"同じ意味を持ちます。

16 進数の 64 ビット値を入力することができます、 **xxxxxxxx\`xxxxxxxx**形式。 アクサン グラーブ記号を省略することもできます (\`)。 アクサン グラーブ記号を含める場合[自動符号拡張](sign-extension.md)は無効です。

### <a name="span-idsymbolsinmasmexpressionsspanspan-idsymbolsinmasmexpressionsspansymbols-in-masm-expressions"></a><span id="symbols_in_masm_expressions"></span><span id="SYMBOLS_IN_MASM_EXPRESSIONS"></span>MASM の式内のシンボル

MASM の式では、任意のシンボルの数値は、そのメモリ アドレスです。 シンボルが参照する対象、によっては、このアドレスは、グローバル変数、ローカル変数、関数、セグメント、モジュール、またはその他の任意の認識されているラベルのアドレスです。

アドレスが関連付けられているモジュールを指定するには、モジュール名とシンボルの名前の前に感嘆符 (!) を含めます。 シンボルは、16 進数として解釈される可能性を場合は、モジュール名や感嘆符シンボル名の前に、感嘆符だけが含まれます。 シンボルの認識の詳細については、次を参照してください。[シンボルの構文と一致するシンボル](symbol-syntax-and-symbol-matching.md)します。

2 つのコロン (:) を使用して、または 2 つのアンダー スコア (\_\_) をクラスのメンバーを示します。

使用して、アクサン グラーブ (\`) やモジュール名と記号の前に感嘆符を追加する場合にのみ、シンボル名のアポストロフィ (')。

### <a name="span-idnumericoperatorsinmasmexpressionsspanspan-idnumericoperatorsinmasmexpressionsspannumeric-operators-in-masm-expressions"></a><span id="numeric_operators_in_masm_expressions"></span><span id="NUMERIC_OPERATORS_IN_MASM_EXPRESSIONS"></span>数値演算子での MASM 式

式の任意のコンポーネントは、単項演算子を使用して変更できます。 二項演算子を使用して、2 つのコンポーネントを組み合わせることができます。 単項演算子は、二項演算子よりも優先されます。 複数の二項演算子を使用する場合、演算子は、次の表で説明されている固定の優先順位規則に従います。

常に、かっこを使用して、優先順位の規則を上書きすることができます。

式はに従って解釈されます MASM 式の一部をかっこで囲まれた式の前に 2 つのアット マーク (@ @) から表示される場合は、[式の C++ 規則](c---numbers-and-operators.md)します。 アット マークから 2 つと左かっこの間にスペースを追加することはできません。 指定することも、[式エバリュエーター](evaluating-expressions.md)を使用して **@@c+ ([...])** または **@@masm([...])**.

算術計算を実行するときに MASM 式エバリュエーターはすべての数字および記号を ULONG64 型として扱います。

単項アドレス演算子は、アドレスの既定のセグメントとして DS を想定しています。 式は、演算子の優先順位の順序で評価されます。 隣接する演算子の優先順位の等しい場合は、式は左から右に評価します。

次のような単項演算子を使用することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>+</p></td>
<td align="left"><p>単項プラス</p></td>
</tr>
<tr class="even">
<td align="left"><p>-</p></td>
<td align="left"><p>単項マイナス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>非</p></td>
<td align="left"><p>引数が 0 の場合は、1 を返します。 0 以外の任意の引数に対して 0 を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>こんにちは</strong></p></td>
<td align="left"><p>上位 16 ビット</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>low</strong></p></td>
<td align="left"><p>低 16 ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>によって</strong></p></td>
<td align="left"><p>指定したアドレスから下位バイト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pby</strong></p></td>
<td align="left"><p>同じ<strong>によって</strong>物理アドレスを受け取る点を除いて。 既定のキャッシュ動作を使用する物理メモリのみを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wo</strong></p></td>
<td align="left"><p>指定したアドレスから下位ワード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pwo</strong></p></td>
<td align="left"><p>同じ<strong>wo</strong>物理アドレスを受け取る点を除いて。 既定のキャッシュ動作を使用する物理メモリのみを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dwo</strong></p></td>
<td align="left"><p>指定したアドレスからダブル ワードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pdwo</strong></p></td>
<td align="left"><p>同じ<strong>dwo</strong>物理アドレスを受け取る点を除いて。 既定のキャッシュ動作を使用する物理メモリのみを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>qwo</strong></p></td>
<td align="left"><p>指定したアドレスからのクアッド単語。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pqwo</strong></p></td>
<td align="left"><p>同じ<strong>qwo</strong>物理アドレスを受け取る点を除いて。 既定のキャッシュ動作を使用する物理メモリのみを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>poi</strong></p></td>
<td align="left"><p>指定したアドレスからポインター-サイズ データ。 ポインターのサイズは、32 ビットまたは 64 ビットです。 カーネルのデバッグでこのサイズのプロセッサに基づいて、<em>ターゲット</em>コンピューター。 Itanium ベースのコンピューターでユーザー モードのデバッグでは、このサイズは 32 ビットまたは 64 ビット、ターゲット アプリケーションによっては。 そのため、 <strong>poi</strong>ポインター-サイズのデータが必要な場合に使用する最適な演算子です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ppoi</strong></p></td>
<td align="left"><p>同じ<strong>poi</strong>物理アドレスを受け取る点を除いて。 既定のキャッシュ動作を使用する物理メモリのみを読み取ることができます。</p></td>
</tr>
</tbody>
</table>

 

次の二項演算子を使用することができます。 各セルに演算子は、下のセルよりも優先されます。 同じセルで演算子が同じ優先順位の左から右に解析されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*</p>
<p>/</p>
<p><strong>mod</strong> (または %)</p></td>
<td align="left"><p>乗算</p>
<p>整数除算</p>
<p>剰余 (余り)</p></td>
</tr>
<tr class="even">
<td align="left"><p>+</p>
<p>-</p></td>
<td align="left"><p>追加</p>
<p>減算</p></td>
</tr>
<tr class="odd">
<td align="left"><p>&lt;&lt;</p>
<p>&gt;&gt;</p>
<p>&gt;&gt;&gt;</p></td>
<td align="left"><p>左シフト</p>
<p>論理の右シフト</p>
<p>算術右シフト</p></td>
</tr>
<tr class="even">
<td align="left"><p>= (または = =)</p>
<p>&lt;</p>
<p>&gt;</p>
<p>&lt;=</p>
<p>&gt;=</p>
<p>!=</p></td>
<td align="left"><p>等しい</p>
<p>次の値未満</p>
<p>より大きい</p>
<p>以下</p>
<p>以上</p>
<p>次の値に等しくない</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>and</strong> (または&amp;)</p></td>
<td align="left"><p>ビットごとの AND</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>xor</strong> (または ^)</p></td>
<td align="left"><p>ビットごとの XOR (排他的 OR)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>または</strong>(または |)</p></td>
<td align="left"><p>ビットごとの OR</p></td>
</tr>
</tbody>
</table>

 

&lt;、 &gt;、=、= =、! = 比較演算子は、式が false の場合、式が true または 0 の場合 1 を評価します。 1 つの等号 (=) では、2 つの等号 (= =) と同じです。 副作用または MASM 式内での割り当てを使用することはできません。

「オペランド エラー」で、(ゼロによる除算) などの無効な操作の結果が返されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-idnonnumericoperatorsinmasmexpressionsspanspan-idnonnumericoperatorsinmasmexpressionsspannon-numeric-operators-in-masm-expressions"></a><span id="non_numeric_operators_in_masm_expressions"></span><span id="NON_NUMERIC_OPERATORS_IN_MASM_EXPRESSIONS"></span>数値以外の演算子での MASM 式

MASM の式で、次の演算子を使用することもできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$fnsucc(</strong><em>FnAddress</em>, <em>RetVal</em>, <em>Flag</em><strong>)</strong></p></td>
<td align="left"><p>解釈、 <em>RetVal</em>値にある関数の戻り値として、 <em>FnAddress</em>アドレス。 この戻り値が、成功コードと見なされる場合<strong>$fnsucc</strong>返します<strong>TRUE</strong>します。 それ以外の場合、 <strong>$fnsucc</strong>返します<strong>FALSE</strong>します。</p>
<p>場合、戻り値の型は、BOOL、bool、ハンドル、HRESULT、または NTSTATUS、 <strong>$fnsucc</strong>返すかどうか、指定された値は"成功"コードとして修飾を正しく認識します。 戻り値の型がポインターである場合は、すべての値以外の<strong>NULL</strong>成功コードとして修飾します。 値によって、他の種類の成功が定義されている<em>フラグ</em>します。 場合<em>フラグ</em>は 0、0 以外の値の<em>RetVal</em>は成功します。 場合<em>フラグ</em>は 1、0 の<em>RetVal</em>は成功します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$iment (</strong><em>アドレス</em><strong>)</strong></p></td>
<td align="left"><p>読み込まれたモジュールの一覧で、イメージのエントリ ポイントのアドレスを返します。 <em>アドレス</em>ポータブル実行可能ファイル (PE) イメージのベース アドレスを指定します。 イメージの PE イメージ ヘッダーにイメージのエントリ ポイントの検索エントリが見つかったを<em>アドレス</em>を指定します。</p>
<p>この関数を使用するには両方のモジュールは既に内でモジュールの一覧を設定する<a href="unresolved-breakpoints---bu-breakpoints-.md" data-raw-source="[unresolved breakpoints](unresolved-breakpoints---bu-breakpoints-.md)">未解決のブレークポイント</a>を使用して、 <strong><a href="bp--bu--bm--set-breakpoint-.md" data-raw-source="[bu](bp--bu--bm--set-breakpoint-.md)">bu</a></strong>コマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scmp("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p>このような-1、0、または 1 に評価される、 <strong>strcmp</strong> C 関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$sicmp("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p>このような-1、0、または 1 に評価される、 <strong>stricmp</strong> Microsoft Win32 関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$spat("</strong><em>String</em><strong>", "</strong><em>Pattern</em><strong>")</strong></p></td>
<td align="left"><p>評価される<strong>TRUE</strong>または<strong>FALSE</strong>かどうかに応じて<em>文字列</em>と一致する<em>パターン</em>します。 大文字と小文字が一致します。 <em>パターン</em>さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$vvalid(</strong><em>Address</em><strong>,</strong> <em>Length</em><strong>)</strong></p></td>
<td align="left"><p>開始されるメモリの範囲かどうかを判断します<em>アドレス</em>の拡張と<em>長さ</em>バイトが無効です。 メモリが、有効な場合は<strong>$vvalid</strong> 1 に評価されます。 メモリが有効でない場合<strong>$vvalid</strong> 0 に評価されます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregistersandpseudoregistersinmasmexpressionsspanspan-idregistersandpseudoregistersinmasmexpressionsspanregisters-and-pseudo-registers-in-masm-expressions"></a><span id="registers_and_pseudo_registers_in_masm_expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_MASM_EXPRESSIONS"></span>レジスタおよび擬似レジスタでの MASM 式

レジスタとの MASM 式内の擬似レジスタを使用することができます。 追加することができます、アット マーク (@) すべてのレジスタと擬似レジスタの前にします。 アット マークと、デバッガーに値をより迅速にアクセスします。 この記号は、最も一般的な x86 ベース レジスタの必要はありません。 その他のレジスタと擬似レジスタを使用して、お勧めを追加すること、アット マークは、実際には必須ではありません。 省略した場合、アット マークは、あまり一般的なレジスタをデバッガーが、16 進数としてし、シンボルとしてのテキストを解析しようとレジスタとして最後にします。

現在の命令ポインターを示すために、ピリオド (.) を使用することもできます。 追加しないでください、アット マークして、その期間の最初のパラメーターとしてピリオドを使用できない前に、 [ **r コマンド**](r--registers-.md)します。 この期間と同じ意味、 **$ip**擬似レジスタ。

レジスタおよび擬似レジスタの詳細については、次を参照してください。[登録構文](register-syntax.md)と[擬似レジスタ構文](pseudo-register-syntax.md)します。

### <a name="span-idsourcelinenumbersinmasmexpressionsspanspan-idsourcelinenumbersinmasmexpressionsspansource-line-numbers-in-masm-expressions"></a><span id="source_line_numbers_in_masm_expressions"></span><span id="SOURCE_LINE_NUMBERS_IN_MASM_EXPRESSIONS"></span>ソース行番号の MASM 式

ソース ファイルと行番号の式内での MASM 式を使用することができます。 グレーブ アクセント記号を使用してこれらの式を囲む必要があります (\`)。 構文の詳細については、次を参照してください。[ソース行構文](source-line-syntax.md)します。

 

 





