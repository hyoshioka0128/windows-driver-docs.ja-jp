---
title: C++ の数値と演算子
description: C++ の数値と演算子
ms.assetid: e5d3ac7f-fd79-48bb-b927-9ad72570dcbe
keywords:
- 式、 C++式の構文
- C++式、数値
- C++式、演算子
- 数値式、C++
- 通信C++
- 優先順位規則C++()
- メソッド
- メソッド、構文
- クラスのメンバー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01c862f6f1d0d3b49c5286ea47a7a4356ca40bd8
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910392"
---
# <a name="c-numbers-and-operators"></a>C++ の数値と演算子


## <span id="ddk_c_numbers_and_operators_dbg"></span><span id="DDK_C_NUMBERS_AND_OPERATORS_DBG"></span>


式C++パーサーでは、すべてのC++形式の式構文がサポートされます。 構文には、すべてのデータ型 (ポインター、浮動小数点数、および配列を含む) C++と、すべての単項演算子と二項演算子が含まれます。

### <a name="span-idnumbers_in_c___expressionsspanspan-idnumbers_in_c___expressionsspannumbers-in-c-expressions"></a><span id="numbers_in_c___expressions"></span><span id="NUMBERS_IN_C___EXPRESSIONS"></span>式のC++数値

式のC++数値は、別の方法で指定しない限り、10進数として解釈されます。 16進数の整数を指定するには、数値の前に**0x**を追加します。 8進数の整数を指定するには、数値の前に**0** (ゼロ) を追加します。

既定のデバッガー基数は、式の入力C++方法には影響しません。 2つの数値を直接入力することはできません ( C++式内に MASM 式を入れ子にする場合を除きます)。

\`<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em><em>形式の</em>16 進数の64ビット値を入力できます。 (アクサングラーブ ( **\`** ) を省略することもできます)。どちらの形式でも同じ値が生成されます。

整数値では、 **L**、 **U**、および**I64**の各サフィックスを使用できます。 作成される数値の実際のサイズは、入力したサフィックスと番号によって異なります。 この解釈の詳細については、 C++ 「言語リファレンス」を参照してください。

式エバリュエーターのC++出力には、 C++式ルールで指定されているデータ型が保持されます。 ただし、この式をコマンドの引数として使用すると、常にキャストが行われます。 たとえば、コマンド引数でアドレスとして使用されている場合、整数値をポインターにキャストする必要はありません。 式の値を整数またはポインターに対して有効なキャストできない場合、構文エラーが発生します。

一部の*出力*には**0n** (10 進数) プレフィックスを使用できますが、式入力C++には使用できません。

### <a name="span-idcharacters_and_strings_in_c___expressionsspanspan-idcharacters_and_strings_in_c___expressionsspancharacters-and-strings-in-c-expressions"></a><span id="characters_and_strings_in_c___expressions"></span><span id="CHARACTERS_AND_STRINGS_IN_C___EXPRESSIONS"></span>式に含まC++れる文字と文字列

単一引用符 (') で囲んで文字を入力できます。 標準C++のエスケープ文字を使用できます。

文字列リテラルは、二重引用符 (") で囲んで入力できます。 **\\"** は、このような文字列内のエスケープシーケンスとして使用できます。 ただし、文字列は[式エバリュエーター](evaluating-expressions.md)には意味がありません。

### <a name="span-idsymbols_in_c___expressionsspanspan-idsymbols_in_c___expressionsspansymbols-in-c-expressions"></a><span id="symbols_in_c___expressions"></span><span id="SYMBOLS_IN_C___EXPRESSIONS"></span>式にC++含まれる記号

C++式では、各記号はその型に従って解釈されます。 シンボルが参照する内容に応じて、整数、データ構造体、関数ポインター、またはその他のデータ型として解釈される場合があります。 C++式内のC++データ型 (変更されていないモジュール名など) に対応しないシンボルを使用すると、構文エラーが発生します。

シンボルがあいまいになる可能性がある場合は、モジュール名と感嘆符 ( **!** )、または記号の前にある感嘆符だけを指します。 シンボル認識の詳細については、「[シンボルの構文と記号の一致](symbol-syntax-and-symbol-matching.md)」を参照してください。

シンボル名の前にモジュール名と感嘆符を追加した場合にのみ、シンボル名にアクサングラーブ ( **\`** ) またはアポストロフィ ( **'** ) を使用できます。

テンプレート名の後に **&lt;** と **&gt;** の区切り記号を追加すると、これらの区切り記号の間にスペースを追加できます。

### <a name="span-idoperators_in_c___expressionsspanspan-idoperators_in_c___expressionsspanoperators-in-c-expressions"></a><span id="operators_in_c___expressions"></span><span id="OPERATORS_IN_C___EXPRESSIONS"></span>式のC++演算子

常にかっこを使用して、優先順位規則をオーバーライドできます。

式のC++一部をかっこで囲み、式の前に2つのアット記号 ( **@@** ) を追加した場合、この式は MASM の式の規則に従って解釈されます。 2つのアット記号と左かっこの間にスペースを追加することはできません。 この式の最終的な値は、ULONG64 値C++として式エバリュエーターに渡されます。 式エバリュエーターは、 **@@c+ + (...)** または **@@masm(.** ..) を使用して指定することもできます。

データ型は、 C++言語で通常どおりに示されます。 配列 ( **\[ \]** )、ポインターメンバー ( **-&gt;** )、UDT メンバー () を示すシンボル **。** )、およびクラス ( **::** ) のメンバーがすべて認識されます。 代入演算子と副作用演算子を含む、すべての算術演算子がサポートされています。 ただし、 **new**、 **delete**、および**throw**演算子は使用できません。実際に関数を呼び出すことはできません。

ポインター演算がサポートされており、オフセットが正しくスケーリングされています。 関数ポインターにオフセットを追加することはできません。 (関数ポインターにオフセットを追加する必要がある場合は、最初にオフセットを文字ポインターにキャストします)。

C++と同様に、無効なデータ型の演算子を使用すると、構文エラーが発生します。 デバッガーのC++式パーサーでは、ほとんどC++のコンパイラよりもやや緩やかなルールが使用されますが、すべての主要なルールが適用されます。 たとえば、整数以外の値をシフトすることはできません。

次の演算子を使用できます。 各セルの演算子は、下位のセルの演算子よりも優先されます。 同じセル内の演算子は同じ優先順位を持ち、左から右に解析されます。 とC++同様に、式の評価は値がわかっている場合に終了します。 このようにすることで、 **myptr \*&** のよう & な式を効果的に使用できるようになります。

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
<td align="left"><p>後続のテキストをすべて無視する</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Class</em> <strong>::</strong> <em>Member</em></p>
<p><em>Class</em> <strong>:: ~</strong><em>Member</em></p>
<p><strong>::</strong> <em>名前</em></p></td>
<td align="left"><p>クラスのメンバー</p>
<p>クラスのメンバー (デストラクター)</p>
<p>グローバル</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>構造体</em> <strong>。</strong> <em>フィールド</em></p>
<p><em>ポインター</em> <strong>-&gt;</strong> <em>フィールド</em></p>
<p><em>名前</em> <strong>[</strong><em>整数</em><strong>]</strong></p>
<p><em>左辺</em>値の<strong>++</strong></p>
<p><em>左辺</em>値の<strong>--</strong></p>
<p><strong>dynamic_cast &lt;</strong><em>型</em><strong>&gt;(</strong><em>値</em><strong>)</strong></p>
<p><strong>static_cast &lt;</strong><em>型</em><strong>&gt;(</strong><em>値</em><strong>)</strong></p>
<p><strong>reinterpret_cast &lt;</strong><em>型</em><strong>&gt;(</strong><em>値</em><strong>)</strong></p>
<p><strong>const_cast &lt;</strong><em>型</em><strong>&gt;(</strong><em>値</em><strong>)</strong></p></td>
<td align="left"><p>構造体のフィールド</p>
<p>参照された構造体のフィールド</p>
<p>配列の添字</p>
<p>インクリメント (評価後)</p>
<p>デクリメント (評価後)</p>
<p>型キャスト (常に実行される)</p>
<p>型キャスト (常に実行される)</p>
<p>型キャスト (常に実行される)</p>
<p>型キャスト (常に実行される)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>(</strong><em>型</em><strong>)</strong> <em>値</em></p>
<p><strong>sizeof</strong> <em>値</em></p>
<p><strong>sizeof (</strong> <em>型</em> <strong>)</strong></p>
<p><strong>++</strong> <em>左辺</em>値</p>
<p><strong>--</strong> <em>左辺</em>値</p>
<p><strong>~</strong> <em>値</em></p>
<p><strong>!</strong> <em>値</em></p>
<p><em>値</em></p>
<p><strong>+</strong><em>値</em></p>
<p><strong>&</strong> <em>左辺</em>値</p>
<p><strong><em></strong><em>値</em></p></td>
<td align="left"><p>型キャスト (常に実行される)</p>
<p>式のサイズ</p>
<p>データ型のサイズ</p>
<p>インクリメント (評価前)</p>
<p>デクリメント (評価前)</p>
<p>ビット補数</p>
<p>Not (ブール値)</p>
<p>単項マイナス</p>
<p>単項プラス</p>
<p>データ型のアドレス</p>
<p>間接</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>構造体</em><strong>。 <em></strong><em>ポインター</em></p>
<p><em>ポインター</em> <strong>-&gt; *</strong> <em>ポインター</em></p></td>
<td align="left"><p>構造体のメンバーへのポインター</p>
<p>参照された構造体のメンバーへのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em><strong></em></strong><em>値</em></p>
<p><em>値</em> <strong>/</strong> <em>値</em></p>
<p><em>値</em> <strong>%</strong> <em>値</em></p></td>
<td align="left"><p>数学</p>
<p>Division (部門)</p>
<p>剰余</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>+</strong>の<em>値</em></p>
<p><em>値</em> <strong>-</strong>の<em>値</em></p></td>
<td align="left"><p>加わっ</p>
<p>減算</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>&lt;&lt;</strong> <em>値</em></p>
<p><em>値</em> <strong>&gt;&gt;</strong> <em>値</em></p></td>
<td align="left"><p>ビットごとのシフト (左)</p>
<p>ビットごとのシフト右</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>&lt;</strong> <em>値</em></p>
<p><em>値</em> <strong>&lt;=</strong> <em>値</em></p>
<p><em>値</em> <strong>&gt;</strong> <em>値</em></p>
<p><em>値</em> <strong>&gt;=</strong> <em>値</em></p></td>
<td align="left"><p>より小さい (比較)</p>
<p>以下 (比較)</p>
<p>より大きい (比較)</p>
<p>以上 (比較)</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>==</strong> <em>値</em></p>
<p><em>値</em> <strong>! =</strong> <em>値</em></p></td>
<td align="left"><p>等しい (比較)</p>
<p>等しくない (比較)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>&</strong> <em>値</em></p></td>
<td align="left"><p>ビットごとの AND</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>^</strong> <em>値</em></p></td>
<td align="left"><p>ビットごとの XOR (排他的 OR)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>|</strong> <em>値</em></p></td>
<td align="left"><p>ビットごとの OR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>値</em> <strong>&&</strong> <em>値</em></p></td>
<td align="left"><p>論理 AND</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>||</strong> <em>値</em></p></td>
<td align="left"><p>論理 OR</p></td>
</tr>
<tr class="even">
<td align="left">
<p><em>左辺</em>値<strong>=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>*=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>/=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>%=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>+=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>-=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>&lt;&lt;=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>&gt;&gt;=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>&=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>|=</strong> <em>値</em></p>
<p><em>左辺</em>値<strong>^=</strong> <em>値</em></p></td>
<td align="left"><p>割り当て</p>
<p>乗算して代入</p>
<p>分割して割り当てる</p>
<p>剰余と代入</p>
<p>追加して割り当てる</p>
<p>減算して代入</p>
<p>左にシフトして割り当てる</p>
<p>右へシフトして割り当てる</p>
<p>AND と assign</p>
<p>または、割り当て</p>
<p>XOR と代入</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>値</em> <strong>?</strong> <em>値</em> <strong>:</strong> <em>値</em></p></td>
<td align="left"><p>条件付き評価</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>、</strong> <em>value</em></p></td>
<td align="left"><p>すべての値を評価し、右端の値以外はすべて破棄します</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregisters_and_pseudo_registers_in_c___expressionsspanspan-idregisters_and_pseudo_registers_in_c___expressionsspanregisters-and-pseudo-registers-in-c-expressions"></a><span id="registers_and_pseudo_registers_in_c___expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_C___EXPRESSIONS"></span>式でのC++レジスタと擬似レジスタ

式内でC++は、レジスタと擬似レジスタを使用できます。 レジスタまたは擬似レジスタの前にアットマーク ( **@** ) を追加する必要があります。

式エバリュエーターは、自動的に適切なキャストを実行します。 実際のレジスタと整数値の擬似レジスタは ULONG64 にキャストされます。 すべてのアドレスが PUCHAR にキャストされます。 **$thread**は ethread\*にキャストされ **$PROC**は ethread\*にキャストされ、 **$teb**は teb\*にキャストされ、$peb は peb\*に**キャストされ**ます。

代入演算子または副作用演算子によってレジスタまたは擬似レジスタを変更することはできません。 これらの値を変更するには、 [**r (レジスタ)** ](r--registers-.md)コマンドを使用する必要があります。

レジスタと擬似レジスタの詳細については、「 [Register 構文](register-syntax.md)」と「[擬似レジスタ構文](pseudo-register-syntax.md)」を参照してください。

### <a name="span-idmacros_in_c___expressionsspanspan-idmacros_in_c___expressionsspanmacros-in-c-expressions"></a><span id="macros_in_c___expressions"></span><span id="MACROS_IN_C___EXPRESSIONS"></span>マクロ ( C++式の)

マクロは、式のC++中で使用できます。 マクロの前に番号記号 (\#) を追加する必要があります。

次のマクロを使用できます。 これらのマクロは、同じ名前を持つ Microsoft Windows マクロと同じ定義を持ちます。 (Windows マクロは、Winnt.h で定義されています)。

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
<td align="left"><p>#CONTAINING_RECORD (<em>Address</em>、 <em>Type</em>、 <em>Field</em>)</p></td>
<td align="left"><p>構造体の型と構造体内のフィールドのアドレスを指定して、構造体のインスタンスのベースアドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#FIELD_OFFSET (<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>既知の構造体型の名前付きフィールドのバイトオフセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_CONTAINS_FIELD (<em>構造体</em>、<em>サイズ</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>指定されたバイトサイズに必要なフィールドが含まれているかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_FIELD_SIZE (<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>フィールドの型を必要としない、既知の型の構造体のフィールドのサイズを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_NUMBER_OF (<em>配列</em>)</p></td>
<td align="left"><p>静的にサイズ設定された配列内の要素の数を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_SIZEOF_THROUGH_FIELD (<em>型</em>、<em>フィールド</em>)</p></td>
<td align="left"><p>指定されたフィールドを含む、既知の型の構造体のサイズを返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





