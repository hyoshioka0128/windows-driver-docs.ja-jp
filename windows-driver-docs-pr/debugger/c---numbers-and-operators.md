---
title: C++ の数値と演算子
description: C++ の数値と演算子
ms.assetid: e5d3ac7f-fd79-48bb-b927-9ad72570dcbe
keywords:
- 式では、C++ 式の構文
- C++ の式、数値
- C++ の式、演算子
- 数値式、C++
- C++ の演算子
- 優先順位の規則 (C++)
- メソッド
- メソッド、構文
- クラスのメンバー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b294b37ad5627b6d7b708552a6da79e89cd6b1c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373961"
---
# <a name="c-numbers-and-operators"></a>C++ の数値と演算子


## <span id="ddk_c_numbers_and_operators_dbg"></span><span id="DDK_C_NUMBERS_AND_OPERATORS_DBG"></span>


C++ の式パーサーには、C++ 式の構文のすべての形式がサポートしています。 (ポインター、浮動小数点数、および配列を含む) すべてのデータ型とすべての C++ 単項および二項演算子、構文が含まれます。

### <a name="span-idnumbersincexpressionsspanspan-idnumbersincexpressionsspannumbers-in-c-expressions"></a><span id="numbers_in_c___expressions"></span><span id="NUMBERS_IN_C___EXPRESSIONS"></span>C++ の式内の番号

C++ の式内の番号は、別の方法でそれらを指定しない限りの 10 進数として解釈されます。 16 進数の整数を指定する追加**0 x**番号の前にします。 8 進数の整数を指定する追加**0**番号の前に (0)。

既定のデバッガーの基数は、C++ の式を入力する方法には影響しません。 2 進数を直接入力することはできません (C++ の式内での MASM 式の入れ子にしてを除く)。

16 進数の 64 ビット値を入力することができます、 <em>xxxxxxxx</em>**\`**<em>xxxxxxxx</em>形式。 (アクサン グラーブ記号を省略することもできます ( **\`** ).)両方の形式は、同じ値を生成します。

使用することができます、 **L**、 **U**と**I64**サフィックスを整数値を使用します。 作成される数の実際のサイズは、サフィックスと、入力した番号に依存します。 この解釈の詳細については、C++ 言語のリファレンスを参照してください。

*出力*C++ の式エバリュエーターが式の C++ 規則を指定するデータ型を保持します。 ただし、コマンドの引数としてこの式を使用する場合、キャスト常に行われます。 たとえば、コマンド引数内のアドレスとして使用している場合は、ポインターに整数値をキャストする必要はありません。 式の値は、お持ちのお客様、整数またはポインターにキャストできません、構文エラーが発生します。

使用することができます、 **0n**一部 (10 進数) のプレフィックス*出力*が、C++ 式の入力に使用することはできません。

### <a name="span-idcharactersandstringsincexpressionsspanspan-idcharactersandstringsincexpressionsspancharacters-and-strings-in-c-expressions"></a><span id="characters_and_strings_in_c___expressions"></span><span id="CHARACTERS_AND_STRINGS_IN_C___EXPRESSIONS"></span>文字と C++ の式の文字列

文字を入力するには、単一引用符 (') で囲みます。 C++ の標準のエスケープ文字が許可されます。

リテラル文字列を入力するには、二重引用符 (") で囲みます。 使用することができます **\\"** このような文字列内のエスケープ シーケンスとして。 ただし、文字列なしにとって意味を持つ、[式エバリュエーター](evaluating-expressions.md)します。

### <a name="span-idsymbolsincexpressionsspanspan-idsymbolsincexpressionsspansymbols-in-c-expressions"></a><span id="symbols_in_c___expressions"></span><span id="SYMBOLS_IN_C___EXPRESSIONS"></span>C++ の式内のシンボル

C++ の式では、各シンボルはその型に従って解釈されます。 によって、シンボルが参照する対象、整数、データ構造体、関数ポインター、またはその他の任意のデータ型として解釈可能性があります。 C++ 式の中で (変更されていないモジュール名) など、C++ データ型に対応していないシンボルを使用する場合は、構文エラーが発生します。

場合は、シンボルが不明確な場合、モジュール名と感嘆符を追加することができます ( **!** ) または記号の前に感嘆符のみです。 シンボルの認識の詳細については、次を参照してください。[シンボルの構文と一致するシンボル](symbol-syntax-and-symbol-matching.md)します。

アクサン グラーブを使用することができます ( **\`** ) またはアポストロフィ ( **'** ) 感嘆符シンボル名の前に、モジュール名を追加する場合にのみ、シンボル名。

追加すると、 **&lt;** と**&gt;** 区切り記号テンプレート名の後に、これらの区切り記号の間にスペースを追加することができます。

### <a name="span-idoperatorsincexpressionsspanspan-idoperatorsincexpressionsspanoperators-in-c-expressions"></a><span id="operators_in_c___expressions"></span><span id="OPERATORS_IN_C___EXPRESSIONS"></span>C++ の式の演算子

常に、かっこを使用して、優先順位の規則を上書きすることができます。

C++ の式の一部をかっこで囲み、2 つのアットを追加する場合 (**@@**)、式の前に、式が MASM 式の規則に従って解釈されます。 アット マークから 2 つと左かっこの間にスペースを追加することはできません。 この式の最終的な値は、C++ の式エバリュエーターに ULONG64 値として渡されます。 使用して、式エバリュエーターを指定することもできます **@@c+ ([...])。** または **@@masm([...])**.

データ型は、通常どおり、C++ 言語で示されます。 配列を示す記号 ( **\[ \]** )、ポインターのメンバー ( **- &gt;** )、UDT のメンバー (**します。** )、およびクラスのメンバー ( **::** ) はすべて認識します。 代入演算子と副作用の演算子を含む、すべての算術演算子をサポートします。 ただし、使用することはできません、**新しい**、**削除**、および**スロー**演算子、およびするにより実際に、関数が呼び出すことはできません。

オフセットが正しく拡大縮小およびポインターの算術演算がサポートされます。 関数ポインターへのオフセットを追加できないことに注意してください。 (関数ポインターにオフセットを追加する場合は、キャスト文字ポインターのオフセットまず。)

C++ では、ように、無効なデータ型で演算子を使用する場合は、構文エラーが発生します。 デバッガーの C++ 式パーサーがほとんどの C++ コンパイラよりも少し緩和された規則を使用しますが、すべての主要な規則が適用されます。 たとえば、整数以外の値を移動することはできません。

次の演算子を使用することができます。 各セルに演算子は、下のセルよりも優先されます。 同じセルで演算子が同じ優先順位の左から右に解析されます。 式の評価は、C++ と同様、その値がわかっている場合を終了します。 この終了などの式を効果的に使用できます。 **?? myPtr & & \*myPtr**します。

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
<td align="left"><p><em>式</em> <strong>//</strong> <em>コメント</em></p></td>
<td align="left"><p>後続のすべてのテキストを無視します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>クラス</em> <strong>:。</strong><em>Member</em></p>
<p><em>クラス</em> <strong>:: ~</strong><em>メンバー</em></p>
<p><strong>::</strong><em>名前</em></p></td>
<td align="left"><p>クラスのメンバー</p>
<p>クラス (デストラクター) のメンバー</p>
<p>グローバル</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>構造体</em><strong>します。</strong> <em>フィールド</em></p>
<p><em>ポインター</em> <strong>- &gt;</strong> <em>フィールド</em></p>
<p><em>Name</em> <strong>[</strong><em>integer</em><strong>]</strong></p>
<p><em>LValue</em> <strong>++</strong></p>
<p><em>LValue</em> <strong>--</strong></p>
<p><strong>dynamic_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>static_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>reinterpret_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>const_cast &lt;</strong> <em>型</em><strong>&gt;(</strong><em>値</em><strong>)</strong></p></td>
<td align="left"><p>構造内のフィールド</p>
<p>参照先の構造体のフィールド</p>
<p>配列の添字</p>
<p>増分 (後の評価)</p>
<p>デクリメント (後の評価)</p>
<p>(常に実行されます) を型キャスト</p>
<p>(常に実行されます) を型キャスト</p>
<p>(常に実行されます) を型キャスト</p>
<p>(常に実行されます) を型キャスト</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>(</strong><em>型</em><strong>)</strong> <em>値</em></p>
<p><strong>sizeof</strong> <em>value</em></p>
<p><strong>sizeof(</strong> <em>type</em> <strong>)</strong></p>
<p><strong>++</strong> <em>LValue</em></p>
<p><strong>--</strong> <em>LValue</em></p>
<p><strong>~</strong> <em>値</em></p>
<p><strong>\!</strong> <em>値</em></p>
<p><em>値</em></p>
<p><strong>+</strong> <em>値</em></p>
<p><strong>&amp;</strong> <em>LValue</em></p>
<p><strong><em></strong> <em>値</em></p></td>
<td align="left"><p>(常に実行されます) を型キャスト</p>
<p>式のサイズ</p>
<p>データ型のサイズ</p>
<p>(評価) の前にインクリメント</p>
<p>(評価) の前にデクリメントします。</p>
<p>ビット補数</p>
<p>しない (ブール値)</p>
<p>単項マイナス</p>
<p>単項プラス</p>
<p>データ型のアドレス</p>
<p>逆参照します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>構造体</em><strong>します。 <em></strong> <em>ポインター</em></p>
<p><em>ポインター</em> <strong>- &gt;  *</strong> <em>ポインター</em></p></td>
<td align="left"><p>構造体のメンバーへのポインター</p>
<p>参照先の構造体のメンバーへのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong> </em></strong> <em>値</em></p>
<p><em>Value</em> <strong>/</strong> <em>Value</em></p>
<p><em>Value</em> <strong>%</strong> <em>Value</em></p></td>
<td align="left"><p>乗算</p>
<p>Division (部門)</p>
<p>剰余</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong> +</strong> <em>値</em></p>
<p><em>値</em> <strong> -</strong> <em>値</em></p></td>
<td align="left"><p>追加</p>
<p>減算</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>&lt; &lt;</strong> <em>値</em></p>
<p><em>値</em> <strong>&gt; &gt;</strong> <em>値</em></p></td>
<td align="left"><p>ビットごとのシフト左</p>
<p>適切なビットごとのシフト</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>&lt;</strong> <em>Value</em></p>
<p><em>値</em> <strong>&lt; =</strong> <em>値</em></p>
<p><em>Value</em> <strong>&gt;</strong> <em>Value</em></p>
<p><em>値</em> <strong>&gt; =</strong> <em>値</em></p></td>
<td align="left"><p>(比較) より小さい</p>
<p>小さい以上 (比較)</p>
<p>(比較) より大きい</p>
<p>大きい以上 (比較)</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>==</strong> <em>Value</em></p>
<p><em>値</em> <strong>! =</strong> <em>値</em></p></td>
<td align="left"><p>等しい (比較)</p>
<p>等しくない (比較)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>&amp;</strong> <em>Value</em></p></td>
<td align="left"><p>ビットごとの AND</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>^</strong> <em>Value</em></p></td>
<td align="left"><p>ビットごとの XOR (排他的 OR)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>|</strong> <em>Value</em></p></td>
<td align="left"><p>ビットごとの OR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>&amp; &amp;</strong> <em>値</em></p></td>
<td align="left"><p>論理 AND</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>||</strong> <em>Value</em></p></td>
<td align="left"><p>論理 OR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>LValue</em> <strong>=</strong><em>Value</em></p>
<p><em>LValue</em> <strong></em>=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>/=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>%=</strong><em>Value</em></p>
<p><em>LValue</em> <strong>+=</strong><em>Value</em></p>
<p><em>LValue</em> <strong>-=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&lt;&lt;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&gt;&gt;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&amp;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>|=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>^=</strong> <em>Value</em></p></td>
<td align="left"><p>割り当てる</p>
<p>乗算して代入.</p>
<p>除算して代入</p>
<p>剰余を割り当てると</p>
<p>追加して割り当てる</p>
<p>減算して代入</p>
<p>左にシフトし、割り当てる</p>
<p>右にシフトして、割り当てる</p>
<p>して割り当てる</p>
<p>または割り当てます</p>
<p>XOR と割り当て</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em><strong>でしょうか。</strong> <em>値</em> <strong>:</strong><em>値</em></p></td>
<td align="left"><p>条件付き評価</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>、</strong> <em>値</em></p></td>
<td align="left"><p>すべての値を評価し、右端の値を除くすべてを破棄し、</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregistersandpseudoregistersincexpressionsspanspan-idregistersandpseudoregistersincexpressionsspanregisters-and-pseudo-registers-in-c-expressions"></a><span id="registers_and_pseudo_registers_in_c___expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_C___EXPRESSIONS"></span>レジスタと C++ の式での擬似レジスタ

レジスタと C++ の式内の擬似レジスタを使用することができます。 追加する必要があります、アット マーク ( **@** ) 登録または擬似レジスタの前にします。

式エバリュエーターでは、適切なキャストが自動的に実行します。 実際のレジスタおよび整数値の擬似レジスタは、ULONG64 にキャストされます。 すべてのアドレスは、PUCHAR にキャスト **$thread** ETHREAD にキャストされます\*、 **$proc** 」プロセスにキャスト\*、 **$teb** TEBにキャスト\*、および **$peb** PEB にキャスト\*します。

登録または擬似レジスタ割り当てまたは副作用演算子によってを変更することはできません。 使用する必要があります、 [ **r (レジスタ)** ](r--registers-.md)これらの値を変更するコマンド。

レジスタおよび擬似レジスタの詳細については、次を参照してください。[登録構文](register-syntax.md)と[擬似レジスタ構文](pseudo-register-syntax.md)します。

### <a name="span-idmacrosincexpressionsspanspan-idmacrosincexpressionsspanmacros-in-c-expressions"></a><span id="macros_in_c___expressions"></span><span id="MACROS_IN_C___EXPRESSIONS"></span>C++ の式内のマクロ

C++ の式内のマクロを使用することができます。 シャープ記号を追加する必要があります (\#)、マクロの前にします。

次のマクロを使用することができます。 これらのマクロは、同じ名前の Microsoft Windows マクロとして同じの定義を指定します。 (Windows マクロは、Winnt.h で定義されます)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">戻り値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>#CONTAINING_RECORD (<em>アドレス</em>、<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>構造体の種類と、構造内のフィールドのアドレス指定構造体のインスタンスのベース アドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#数値フィールド オフセット (<em>型</em>、<em>フィールド</em>)。</p></td>
<td align="left"><p>既知の構造体の型では、名前付きフィールドのバイト オフセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_CONTAINS_FIELD (<em>構造体</em>、<em>サイズ</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>指定したバイト サイズが、必要なフィールドを含むかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_FIELD_SIZE (<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>フィールドの型を必要とせず、既知の型の構造体のフィールドのサイズを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_NUMBER_OF(<em>Array</em>)</p></td>
<td align="left"><p>静的にサイズの配列内の要素の数を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_SIZEOF_THROUGH_FIELD (<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>指定したフィールドも含めてを既知の型の構造体のサイズを返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





