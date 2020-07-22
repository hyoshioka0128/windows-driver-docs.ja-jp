---
title: MASM の数値と演算子
description: MASM の数値と演算子
ms.assetid: 9aeb3ef2-d83a-4f99-9a55-4bbd8a7e11b5
keywords:
- 式、MASM 式の構文
- 数値式 (MASM)
- MASM の式、数値
- MASM 式、演算子
- 演算子 (MASM)
- (MASM プレフィックス)
- 二項演算子
- シフト演算子
- 単項演算子
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b19be1872c67d7228822a6262cf9bcfa976ba70
ms.sourcegitcommit: 67fb9981ca51df198dfb6af9bf4987843266f8ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86879088"
---
# <a name="masm-numbers-and-operators"></a>MASM の数値と演算子

Windows package、NTSD、CDB、KD、および WinDbg のデバッグツールのバージョン4.0 より前は、Microsoft マクロアセンブラ (MASM) 式構文のみが使用されていました。

## <a name="numbers-in-masm-expressions"></a>MASM 式の数値

MASM の式には、16、10、8、または2の基数で数値を入力できます。

[**N (Set Number Base)**](n--set-number-base-.md)コマンドを使用して、既定の基数を16、10、または8に設定します。 プレフィックスのないすべての数字は、このベースで解釈されます。 既定の基数は、 **0x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0t**プレフィックス (バイナリ) を指定することによってオーバーライドできます。

数値の後に**h**を追加することによって、16進数の数値を指定することもできます。 数字の中で大文字または小文字を使用できます。 たとえば、"0x4AB3"、"0X4aB3"、"4AB3h"、"4AB3h"、および "4aB3H" は同じ意味を持ちます。

式のプレフィックスの後に数字を追加しない場合、数値は0として読み取られます。 したがって、0を0として、プレフィックスの後に0を、プレフィックスだけを書き込むことができます。 たとえば、16進数では、"0"、"0x0"、および "0x" は同じ意味を持ちます。

**Xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx \` **形式の16進64ビット値を入力できます。 また、アクサングラーブ () を省略することもでき \` ます。 アクサングラーブを含めると、[自動署名拡張機能](sign-extension.md)は無効になります。

## <a name="symbols-in-masm-expressions"></a>MASM 式のシンボル

MASM 式では、任意のシンボルの数値はそのメモリアドレスです。 シンボルが参照する内容に応じて、このアドレスはグローバル変数、ローカル変数、関数、セグメント、モジュール、またはその他の認識されたラベルのアドレスになります。

アドレスが関連付けられているモジュールを指定するには、モジュール名と、シンボルの名前の前に感嘆符 (!) を含めます。 シンボルが16進数として解釈される場合は、モジュール名と感嘆符、または感嘆符だけをシンボル名の前に含めます。 シンボル認識の詳細については、「[シンボルの構文と記号の一致](symbol-syntax-and-symbol-matching.md)」を参照してください。

2つのコロン (::) を使用します。または、2つのアンダースコア ( \_ \_ ) を指定して、クラスのメンバーを示します。

シンボル \` の前にモジュール名と感嘆符を追加した場合にのみ、シンボル名にアクサングラーブ () またはアポストロフィ (') を使用してください。

## <a name="numeric-operators-in-masm-expressions"></a>MASM 式の数値演算子

単項演算子を使用すると、式の任意のコンポーネントを変更できます。 二項演算子を使用すると、任意の2つのコンポーネントを組み合わせることができます。 単項演算子は二項演算子よりも優先されます。 複数の二項演算子を使用する場合、演算子は、次の表で説明されている固定優先順位の規則に従います。

常にかっこを使用して、優先順位規則をオーバーライドできます。

MASM 式の一部がかっこで囲まれ、式の前に2つのアットマーク (@ @) がある場合、式は[C++ の式の規則](c---numbers-and-operators.md)に従って解釈されます。 2つのアット記号と左かっこの間にスペースを追加することはできません。 [式エバリュエーター](evaluating-expressions.md)は、 **@ @c + + (...)** または **@ @masm (.**..) を使用して指定することもできます。

算術計算を実行すると、MASM 式エバリュエーターは、すべての数値と記号を ULONG64 型として扱います。

単項アドレス演算子は、DS をアドレスの既定のセグメントと見なします。 式は、演算子の優先順位に従って評価されます。 隣接する演算子の優先順位が同じ場合、式は左から右に評価されます。

次の単項演算子を使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">意味</th>
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
<td align="left"><p>not</p></td>
<td align="left"><p>引数が0の場合は1を返します。 0以外の任意の引数に対して0を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>hi</strong></p></td>
<td align="left"><p>上位16ビット</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>低画質</strong></p></td>
<td align="left"><p>下位16ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>by</strong></p></td>
<td align="left"><p>指定したアドレスの下位バイト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pby</strong></p></td>
<td align="left"><p>物理アドレスを受け取る点を除い<strong>て、</strong>と同じです。 既定のキャッシュ動作を使用する物理メモリだけを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>フロー</strong></p></td>
<td align="left"><p>指定されたアドレスの下位ワード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pwo</strong></p></td>
<td align="left"><p>物理アドレスを受け取る点を除いて、 <strong>wo</strong>と同じです。 既定のキャッシュ動作を使用する物理メモリだけを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dwo</strong></p></td>
<td align="left"><p>指定されたアドレスからのダブルワード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pdwo</strong></p></td>
<td align="left"><p>物理アドレスを受け取る点を除いて、 <strong>dwo</strong>と同じです。 既定のキャッシュ動作を使用する物理メモリだけを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>qwo</strong></p></td>
<td align="left"><p>指定されたアドレスからのクワッドワード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pqwo</strong></p></td>
<td align="left"><p>物理アドレスを受け取る点を除いて、 <strong>qwo</strong>と同じです。 既定のキャッシュ動作を使用する物理メモリだけを読み取ることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>poi</strong></p></td>
<td align="left"><p>指定されたアドレスからのポインターサイズのデータ。 ポインターのサイズは32ビットまたは64ビットです。 カーネルデバッグでは、このサイズは<em>ターゲット</em>コンピューターのプロセッサに基づいています。 Itanium ベースのコンピューターでのユーザーモードのデバッグでは、ターゲットアプリケーションに応じて、このサイズは32ビットまたは64ビットになります。 そのため、 <strong>poi</strong>は、ポインターサイズのデータが必要な場合に使用するのに最適な演算子です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ppoi</strong></p></td>
<td align="left"><p>物理アドレスを受け取ることを除いて、 <strong>poi</strong>と同じです。 既定のキャッシュ動作を使用する物理メモリだけを読み取ることができます。</p></td>
</tr>
</tbody>
</table>


次の二項演算子を使用できます。 各セルの演算子は、下位のセルの演算子よりも優先されます。 同じセル内の演算子は同じ優先順位を持ち、左から右に解析されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*</p>
<p>/</p>
<p><strong>mod</strong> (または%)</p></td>
<td align="left"><p>乗算</p>
<p>整数の除算</p>
<p>剰余 (剰余)</p></td>
</tr>
<tr class="even">
<td align="left"><p>+</p>
<p>-</p></td>
<td align="left"><p>加算</p>
<p>減算</p></td>
</tr>
<tr class="odd">
<td align="left"><p>&lt;&lt;</p>
<p>&gt;&gt;</p>
<p>&gt;&gt;&gt;</p></td>
<td align="left"><p>左シフト</p>
<p>論理右シフト</p>
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
<p>より小さい</p>
<p>より大きい</p>
<p>以下</p>
<p>以上</p>
<p>等しくない</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>and</strong> (または &)</p></td>
<td align="left"><p>ビット演算子 AND</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>xor</strong> (または ^)</p></td>
<td align="left"><p>ビットごとの XOR (排他的 OR)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>or</strong> (or |)</p></td>
<td align="left"><p>ビットごとの OR</p></td>
</tr>
</tbody>
</table>


&lt;、、 &gt; =、= =、および! = 比較演算子は、式が true の場合は1に、式が false の場合は0に評価されます。 1つの等号 (=) は、2つの等号 (= =) と同じです。 MASM 式の中で副作用や代入を使用することはできません。

無効な操作 (0 による除算など) が発生すると、[デバッガーコマンドウィンドウ](debugger-command-window.md)に "オペランドエラー" が返されます。

### <a name="span-idnon_numeric_operators_in_masm_expressionsspanspan-idnon_numeric_operators_in_masm_expressionsspannon-numeric-operators-in-masm-expressions"></a><span id="non_numeric_operators_in_masm_expressions"></span><span id="NON_NUMERIC_OPERATORS_IN_MASM_EXPRESSIONS"></span>MASM 式での非数値演算子

また、MASM 式では、次の追加演算子を使用することもできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">演算子</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$fnsucc (</strong><em>FnAddress</em>、 <em>RetVal</em>、<em>フラグ</em><strong>)</strong></p></td>
<td align="left"><p><em>RetVal</em>値を、 <em>FnAddress</em>アドレスにある関数の戻り値として解釈します。 この戻り値が成功コードとして修飾されている場合、 <strong>$fnsucc</strong>は<strong>TRUE</strong>を返します。 それ以外の場合、 <strong>$fnsucc</strong>は<strong>FALSE</strong>を返します。</p>
<p>戻り値の型が BOOL、bool、HANDLE、HRESULT、または NTSTATUS の場合、指定した戻り値が成功コードとして修飾されているかどうかを正しく認識<strong>$fnsucc</strong>ます。 戻り値の型がポインターの場合、 <strong>NULL</strong>以外のすべての値は成功コードとして修飾されます。 それ以外の型の場合、success は<em>Flag</em>の値によって定義されます。 <em>フラグ</em>が0の場合、 <em>RetVal</em>の0以外の値は success になります。 <em>フラグ</em>が1の場合、 <em>RetVal</em>のゼロ値は success になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$iment (</strong><em>アドレス</em><strong>)</strong></p></td>
<td align="left"><p>読み込まれたモジュールリスト内のイメージのエントリポイントのアドレスを返します。 <em>アドレス</em>ポータブル実行可能 (PE) イメージのベースアドレスを指定します。 エントリは、その<em>アドレス</em>が指定するイメージの PE イメージヘッダーにあるイメージのエントリポイントを検索することによって検出されます。</p>
<p>この関数は、モジュールリストに既に存在するモジュールに対して使用でき、 <strong><a href="bp--bu--bm--set-breakpoint-.md" data-raw-source="[bu](bp--bu--bm--set-breakpoint-.md)">bu</a></strong>コマンドを使用して<a href="unresolved-breakpoints---bu-breakpoints-.md" data-raw-source="[unresolved breakpoints](unresolved-breakpoints---bu-breakpoints-.md)">未解決のブレークポイント</a>を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scmp ("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p><strong>Strcmp</strong> C 関数のように、-1、0、または1に評価されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$sicmp ("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p><strong>Stricmp</strong> Microsoft Win32 関数のように、-1、0、または1に評価されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$spat ("</strong><em>String</em><strong>", "</strong><em>Pattern</em><strong>")</strong></p></td>
<td align="left"><p><em>文字列</em>が<em>パターン</em>に一致するかどうかによって、 <strong>TRUE</strong>または<strong>FALSE</strong>に評価されます。 照合では大文字と小文字が区別されません。 <em>パターン</em>には、さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、「<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列ワイルドカード構文</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$vvalid (</strong><em>アドレス</em><strong>、</strong> <em>長さ</em><strong>)</strong></p></td>
<td align="left"><p><em>アドレス</em>で始まるメモリ範囲と<em>長さ</em>バイトの拡張を有効にするかどうかを決定します。 メモリが有効な場合、 <strong>$vvalid</strong>は1に評価されます。 メモリが無効な場合、 <strong>$vvalid</strong>は0に評価されます。</p></td>
</tr>
</tbody>
</table>

## <a name="registers-and-pseudo-registers-in-masm-expressions"></a>MASM 式でのレジスタと擬似レジスタ

MASM 式では、レジスタと擬似レジスタを使用できます。 すべてのレジスタと擬似レジスタの前にアットマーク (@) を追加できます。 アットマークを付けると、デバッガーはより迅速に値にアクセスします。 このアットマークは、最も一般的な x86 ベースのレジスタには必要ありません。 他のレジスタや擬似レジスタの場合は、アットマークを追加することをお勧めしますが、実際には必要ありません。 あまり一般的でないレジスタに対してアットマークを省略した場合、デバッガーはテキストを16進数として解析し、次に記号として、最後にレジスタとして解析しようとします。

また、ピリオド (.) を使用して、現在の命令ポインターを示すこともできます。 この期間の前にアットマークを追加することはできません。また、 [**r コマンド**](r--registers-.md)の最初のパラメーターとしてピリオドを使用することはできません。 この期間は **$ip**擬似レジスタと同じ意味になります。

レジスタと擬似レジスタの詳細については、「 [Register 構文](register-syntax.md)」と「[擬似レジスタ構文](pseudo-register-syntax.md)」を参照してください。

## <a name="source-line-numbers-in-masm-expressions"></a>MASM 式のソース行番号

MASM 式では、ソースファイルと行番号の式を使用できます。 これらの式は、アクサングラーブ () を使用して囲む必要があり \` ます。 構文の詳細については、「 [Source Line 構文](source-line-syntax.md)」を参照してください。

