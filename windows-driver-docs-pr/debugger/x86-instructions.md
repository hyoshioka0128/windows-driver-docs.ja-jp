---
title: x86 の手順
description: x86 の手順
ms.assetid: 237796d5-ef82-4eab-8d56-3191b3e63597
keywords:
- x86 プロセッサ、手順
- x86 プロセッサ、算術
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f900c371825dcf7996b6e72bd15c1ad42f7a59
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284924"
---
# <a name="x86-instructions"></a>x86 の手順


## <span id="ddk_x86_instructions_dbg"></span><span id="DDK_X86_INSTRUCTIONS_DBG"></span>


このセクションの一覧では、アスタリスク ( **\*** ) でマークされた手順が特に重要です。 マークされていない手順は、重要ではありません。

X86 プロセッサでは、命令は可変サイズになっているため、逆アセンブルはパターンマッチングの演習です。 アドレスから逆アセンブルするには、先に進んだ時点で逆アセンブルを開始してから、指示がわかり始めるまで進みます。 命令の途中で逆アセンブルを開始した可能性があるため、最初のいくつかの手順では意味がない場合があります。 残念ながら、逆アセンブリが命令ストリームと同期されることはないため、動作する開始点が見つかるまでは、別の開始点で逆アセンブルを試みる必要があります。

適切にパックされた**switch**ステートメントの場合、コンパイラはデータを直接コードストリームに出力するため、 **switch**ステートメントを使用して逆アセンブルすると、通常は、(実際にはデータであるため) 意味のない命令を遭遇ます。 データの末尾を検索し、そこでの逆アセンブルを続行します。

### <a name="span-idinstruction_notationspanspan-idinstruction_notationspanspan-idinstruction_notationspaninstruction-notation"></a><span id="Instruction_Notation"></span><span id="instruction_notation"></span><span id="INSTRUCTION_NOTATION"></span>命令の表記

手順の一般的な表記法としては、コピー先のレジスタを左に配置し、ソースを右側に配置します。 ただし、このルールにはいくつかの例外があります。

通常、算術命令は、コピー元とコピー先のレジスタを組み合わせる2レジスタです。 結果は、変換先に格納されます。

一部の手順には、16ビットバージョンと32ビットバージョンがありますが、ここには32ビットバージョンのみが記載されています。 ここに記載されていないのは、浮動小数点命令、特権命令、およびセグメント化されたモデル (Microsoft Win32 では使用しない) でのみ使用される命令です。

領域を節約するために、次の例に示すように、多くの命令が結合された形式で表されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m/#n</p></td>
<td align="left"><p>r1 = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

は、最初のパラメーターがレジスタである必要がありますが、2番目のパラメーターにはレジスタ、メモリ参照、またはイミディエイト値を指定できます。

さらに多くの領域を節約するために、次のように命令を表現することもできます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

つまり、最初のパラメーターをレジスタまたはメモリ参照にすることができ、2番目のパラメーターにはレジスタ、メモリ参照、またはイミディエイト値を指定できます。

特に明記されていない限り、この省略形を使用する場合は、変換元と変換先の両方に対してメモリを選択することはできません。

さらに、パラメーターがそのサイズである必要があることを示すために、転送元または転送先にビットサイズのサフィックス (8、16、32) を追加できます。 たとえば、r8 は8ビットレジスタを意味します。

### <a name="span-idmemory__data_transfer__and_data_conversionspanspan-idmemory__data_transfer__and_data_conversionspanspan-idmemory__data_transfer__and_data_conversionspanmemory-data-transfer-and-data-conversion"></a><span id="Memory__Data_Transfer__and_Data_Conversion"></span><span id="memory__data_transfer__and_data_conversion"></span><span id="MEMORY__DATA_TRANSFER__AND_DATA_CONVERSION"></span>メモリ、データ転送、データ変換

メモリおよびデータ転送命令は、フラグには影響しません。

### <a name="span-ideffective_addressspanspan-ideffective_addressspanspan-ideffective_addressspaneffective-address"></a><span id="Effective_Address"></span><span id="effective_address"></span><span id="EFFECTIVE_ADDRESS"></span>有効なアドレス

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>戻せるよう</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p>有効なアドレスを読み込みます。</p>
<p>(r = m のアドレス)</p></td>
</tr>
</tbody>
</table>

 

たとえば、 **lea eax \[、esi +\] 4**は**eax** = **esi** + 4 を意味します。 この命令は、多くの場合、算術演算を実行するために使用されます。

### <a name="span-iddata_transferspanspan-iddata_transferspanspan-iddata_transferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>データ転送

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>MOVSX</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>符号拡張を使用して移動します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOVZX</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>拡張子をゼロにして移動します。</p></td>
</tr>
</tbody>
</table>

 

**Movsx**と**movsx**は、ソースから宛先に符号拡張またはゼロ拡張子を実行する、 **mov**命令の特別なバージョンです。 これは、変換元と変換先が異なるサイズになるようにする唯一の命令です。 (実際には、サイズが異なる必要があります。

### <a name="span-idstack_manipulationspanspan-idstack_manipulationspanspan-idstack_manipulationspanstack-manipulation"></a><span id="Stack_Manipulation"></span><span id="stack_manipulation"></span><span id="STACK_MANIPULATION"></span>スタック操作

スタックは**esp**レジスタによってポイントされます。 **Esp**の値はスタックの一番上にあり (最後にプッシュされ、最初にポップされます)。古いスタック要素は、より上位のアドレスに配置します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>押し付け</p></td>
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>値をスタックにプッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>ショート</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>スタックからポップ値を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>PUSHFD</p></td>
<td align="left"></td>
<td align="left"><p>フラグをスタックにプッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>POPFD</p></td>
<td align="left"></td>
<td align="left"><p>スタックからポップフラグを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>PUSHAD</p></td>
<td align="left"></td>
<td align="left"><p>すべての整数レジスタをプッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>POPAD</p></td>
<td align="left"></td>
<td align="left"><p>すべての整数レジスタをポップします。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>Enter</p></td>
<td align="left"><p>#n、#n</p></td>
<td align="left"><p>ビルドスタックフレーム。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>出る</p></td>
<td align="left"></td>
<td align="left"><p>スタックフレームの破棄</p></td>
</tr>
</tbody>
</table>

 

C/C++コンパイラでは、 **enter**命令は使用されません。 ( **Enter**命令は、入れ子になったプロシージャを Algol や Pascal などの言語で実装するために使用されます)。

**Leave**命令は、次の場合と同じです。

```asm
mov esp, ebp
pop ebp
```

### <a name="span-iddata_conversionspanspan-iddata_conversionspanspan-iddata_conversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>データ変換

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CBW</p></td>
<td align="left"><p>Byte (<strong>al</strong>) を word (<strong>ax</strong>) に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CWD</p></td>
<td align="left"><p>Word (<strong>ax</strong>) を dword (<strong>dx</strong>:<strong>ax</strong>) に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CWDE</p></td>
<td align="left"><p>Word (<strong>ax</strong>) を dword (<strong>eax</strong>) に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CDQ</p></td>
<td align="left"><p>dword (<strong>eax</strong>) を qword (<strong>edx</strong>:<strong>eax</strong>) に変換します。</p></td>
</tr>
</tbody>
</table>

 

すべての変換は、符号拡張を実行します。

### <a name="span-idarithmetic_and_bit_manipulationspanspan-idarithmetic_and_bit_manipulationspanspan-idarithmetic_and_bit_manipulationspanarithmetic-and-bit-manipulation"></a><span id="Arithmetic_and_Bit_Manipulation"></span><span id="arithmetic_and_bit_manipulation"></span><span id="ARITHMETIC_AND_BIT_MANIPULATION"></span>算術演算とビット操作

すべての算術およびビット操作命令は、フラグを変更します。

### <a name="span-idarithmeticspanspan-idarithmeticspanspan-idarithmeticspanarithmetic"></a><span id="Arithmetic"></span><span id="arithmetic"></span><span id="ARITHMETIC"></span>数値

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>ADD</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>ADC</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/#n + キャリー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>サブ</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>SBB</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n + キャリー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>NEG</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m =-<strong>r1</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>◇</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m + = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>ALPHA</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m-= 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CMP</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>Compute <strong>r1</strong>/m- <strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**Cmp**命令は減算を計算し、結果に従ってフラグを設定しますが、結果をスローします。 通常は、減算の結果をテストする条件付き**ジャンプ**命令が続きます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>ax</strong> = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>:<strong>ax</strong> = <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>:<strong>eax</strong> = <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>ax</strong> = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>:<strong>ax</strong> = <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>:<strong>eax</strong> = <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m</p></td>
<td align="left"><p>r1 *= <strong>r2</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、#n</p></td>
<td align="left"><p>r1 = <strong>r2</strong>/m * #n</p></td>
</tr>
</tbody>
</table>

 

符号なし乗算と符号付き乗算。 乗算後のフラグの状態は未定義です。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>(<strong>ah</strong>、 <strong>al</strong>) = (<strong>ax</strong> % <strong>r</strong>/m8、 <strong>ax</strong> / <strong>r</strong>/m8)</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p>(<strong>dx</strong>、 <strong>ax</strong>) = <strong>dx</strong>:<strong>ax</strong> / <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p>(<strong>edx</strong>, <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>(<strong>ah</strong>、 <strong>al</strong>) = <strong>ax</strong> / <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p>(<strong>dx</strong>、 <strong>ax</strong>) = <strong>dx</strong>:<strong>ax</strong> / <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p>(<strong>edx</strong>, <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
</tr>
</tbody>
</table>

 

符号なしおよび符号付き除算。 擬似コードの説明の最初のレジスタは余りを受け取り、2番目のレジスタは商を受け取ります。 結果が変換先をオーバーフローした場合、除算オーバーフロー例外が生成されます。

除算後のフラグの状態は未定義です。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>*</p></td>
<td align="left"><p>[<em>Cc</em>の設定]</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>R</strong>/m8 を0または1に設定します</p></td>
</tr>
</tbody>
</table>

 

条件*cc*が true の場合は、8ビット値が1に設定されます。 それ以外の場合は、8ビットの値が0に設定されます。

### <a name="span-idbinary-coded_decimalspanspan-idbinary-coded_decimalspanspan-idbinary-coded_decimalspanbinary-coded-decimal"></a><span id="Binary-coded_Decimal"></span><span id="binary-coded_decimal"></span><span id="BINARY-CODED_DECIMAL"></span>バイナリでコード化された10進数

COBOL で記述されたコードをデバッグする場合を除き、これらの手順は表示されません。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>DAA</p></td>
<td align="left"><p>加算後の小数点の調整。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>型</p></td>
<td align="left"><p>減算後の小数点調整。</p></td>
</tr>
</tbody>
</table>

 

次の手順では、パックされたバイナリでエンコードされた10進数演算を実行した後に、 **al**レジスタを調整します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAA</p></td>
<td align="left"><p>加算後に ASCII で調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAS</p></td>
<td align="left"><p>減算後の ASCII を調整します。</p></td>
</tr>
</tbody>
</table>

 

これらの手順では、展開されたバイナリコード化された10進数演算を実行した後に**al**レジスタを調整します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAM</p></td>
<td align="left"><p>乗算後に ASCII で調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAD</p></td>
<td align="left"><p>除算後に ASCII で調整します。</p></td>
</tr>
</tbody>
</table>

 

これらの手順では、展開されたバイナリコード化された10進数演算を実行した後に**al**レジスタと**ah**レジスタを調整します。

### <a name="span-idbitsspanspan-idbitsspanspan-idbitsspanbits"></a><span id="Bits"></span><span id="bits"></span><span id="BITS"></span>列

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>AND</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m および<strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>スイッチまたは</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m または<strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>XOR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m xor <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>NOT</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m = ビットごとの not <strong>r1</strong>/m</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>TEST</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>Compute <strong>r1</strong>/m および<strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**テスト**命令は論理 AND 演算子を計算し、結果に従ってフラグを設定しますが、結果をスローします。 通常は、論理 AND の結果をテストする条件付きジャンプ命令が続きます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>SHL</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &lt; cl&lt;/#n = </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SHR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; cl&gt;/#n ゼロ-塗りつぶし = </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>SAR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; cl&gt;/#n sign-fill = </p></td>
</tr>
</tbody>
</table>

 

最後にシフトしたビットは、キャリーに配置されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SHLD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>左の double をシフトします。</p></td>
</tr>
</tbody>
</table>

 

**R2**の最上位ビットを入力して、 **r1**を**cl**/\#n 別にシフトします。/m 最後にシフトしたビットは、キャリーに配置されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>SHRD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>Shift right double。</p></td>
</tr>
</tbody>
</table>

 

**R2**の最下位ビットを入力して、 **r1**を**cl**/\#n で右にシフトします。/m 最後にシフトしたビットは、キャリーに配置されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ROL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>を<strong>cl</strong>/#n で左に回転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROR</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>を<strong>cl</strong>/#n で右に回転します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CRL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>/c を<strong>cl</strong>/#n で左に回転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RCR</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>/c を<strong>cl</strong>/#n で右に回転します。</p></td>
</tr>
</tbody>
</table>

 

回転は、シフトされたビットが受信フィルビットとして再表示される点を除いて、シフトに似ています。 C 言語バージョンのローテーション命令では、回転にキャリービットが組み込まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>BT</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>のビット<strong>r2</strong>/#n をキャリーにコピーします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BTS</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>のビット<strong>r2</strong>/#n を設定し、前の値をキャリーにコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BTC</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p><strong>R1</strong>のビット<strong>r2</strong>/#n をクリアし、前の値をキャリーにコピーします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrol_flowspanspan-idcontrol_flowspanspan-idcontrol_flowspancontrol-flow"></a><span id="Control_Flow"></span><span id="control_flow"></span><span id="CONTROL_FLOW"></span>制御フロー

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>J<em>cc</em></p></td>
<td align="left"><p>先</p></td>
<td align="left"><p>分岐条件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p>先</p></td>
<td align="left"><p>ジャンプダイレクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>間接的にジャンプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p>先</p></td>
<td align="left"><p>Direct を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>間接的に呼び出します。</p></td>
</tr>
</tbody>
</table>

 

**呼び出し**命令は、戻りアドレスをスタックにプッシュし、変換先にジャンプします。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>RET</p></td>
<td align="left"><p><em>#非該当</em></p></td>
<td align="left"><p>戻り値</p></td>
</tr>
</tbody>
</table>

 

**Ret**命令は、スタック上の戻りアドレスにポップし、ジャンプします。 **RET**命令内の0以外 *\#の n*は、戻りアドレスをポップした後、値 *\#n*をスタックポインターに追加する必要があることを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ループ</p></td>
<td align="left"><p><strong>Ecx</strong>をデクリメントし、result が0以外の場合はジャンプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LOOPZ</p></td>
<td align="left"><p>結果が0以外で<strong>zr</strong>が設定されている場合、 <strong>ecx</strong>をデクリメントし、ジャンプします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LOOPNZ</p></td>
<td align="left"><p><strong>Ecx</strong>をデクリメントし、結果が0以外で<strong>zr</strong>が明確であった場合にジャンプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>JECXZ</p></td>
<td align="left"><p><strong>Ecx</strong>が0の場合は、ジャンプします。</p></td>
</tr>
</tbody>
</table>

 

これらの手順は x86's CISC の内容の残りの部分であり、最近のプロセッサでは、長い方法で記述された同等の命令よりも実際には遅くなります。

### <a name="span-idstring_manipulationspanspan-idstring_manipulationspanspan-idstring_manipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>文字列操作

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MOVS<em>T</em></p></td>
<td align="left"><p><em>T</em>を<strong>esi</strong>から edi に移動<strong>します。</strong></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>CMPS<em>T</em></p></td>
<td align="left"><p><strong>Esi</strong>と edi<em>を</em>比較<strong>します。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SCAS<em>T</em></p></td>
<td align="left"><p><strong>Edi</strong> for acc<em>をスキャン</em><em>します。</em></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>LODS<em>T</em></p></td>
<td align="left"><p><strong>Esi</strong>から Acc に<em>t</em>を読み込み<em>ます。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>STOS<em>T</em></p></td>
<td align="left"><p>Acc から<strong>edi</strong>に<em>t</em>を格納<em>します。</em></p></td>
</tr>
</tbody>
</table>

 

操作を実行すると、方向フラグ (上または下) の設定に従って、ソースとターゲットのレジスタが sizeof (*T*) によってインクリメントまたはデクリメントされます。

この命令の前に、 **REP** **レジスタに**よって指定された回数だけ操作を繰り返すことができます。

**Rep mov**命令は、メモリのブロックをコピーするために使用されます。

**Rep stos**命令は、メモリのブロックに acc を設定するために使用*されます*。

### <a name="span-idflagsspanspan-idflagsspanspan-idflagsspanflags"></a><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>示す

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>LAHF</p></td>
<td align="left"><p>フラグから<strong>ah</strong>を読み込みます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SAHF</p></td>
<td align="left"><p><strong>Ah</strong>をフラグに格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STC</p></td>
<td align="left"><p>キャリーを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLC</p></td>
<td align="left"><p>キャリーをクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMC</p></td>
<td align="left"><p>補数のキャリー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>商品</p></td>
<td align="left"><p>方向を down に設定<em>します。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLD</p></td>
<td align="left"><p>方向を上に設定<em>します。</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>飛行</p></td>
<td align="left"><p>割り込みを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLI (CLI)</p></td>
<td align="left"><p>割り込みを無効にします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinterlocked_instructionsspanspan-idinterlocked_instructionsspanspan-idinterlocked_instructionsspaninterlocked-instructions"></a><span id="Interlocked_Instructions"></span><span id="interlocked_instructions"></span><span id="INTERLOCKED_INSTRUCTIONS"></span>インタロック命令

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>XCHG</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p><strong>R1</strong>と<strong>r</strong>/m のスワップ</p></td>
</tr>
<tr class="even">
<td align="left"><p>XADD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p><strong>R1</strong>を<strong>r</strong>/m に追加し、元の値を r1 に配置し<strong>ます。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMPXCHG</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>条件を比較して交換します。</p></td>
</tr>
</tbody>
</table>

 

**Cmpxchg**命令は、次のアトミックバージョンです。

```asm
   cmp     accT, r/m
   jz      match
   mov     accT, r/m
   jmp     done
match:
   mov     r/m, r1
done:
```

### <a name="span-idmiscellaneousspanspan-idmiscellaneousspanspan-idmiscellaneousspanmiscellaneous"></a><span id="Miscellaneous"></span><span id="miscellaneous"></span><span id="MISCELLANEOUS"></span>な

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>INT</p></td>
<td align="left"><p>#非該当</p></td>
<td align="left"><p>カーネルにトラップします。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>バインディング</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p><strong>R</strong>が範囲内にない場合にトラップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>NOP</p></td>
<td align="left"></td>
<td align="left"><p>操作は実行されません。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>XLATB</p></td>
<td align="left"></td>
<td align="left"><p><strong>al</strong> = [<strong>ebx</strong> + <strong>al</strong>]</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>BSWAP</p></td>
<td align="left"><p><strong>r</strong></p></td>
<td align="left"><p>レジスタにバイト順序をスワップします。</p></td>
</tr>
</tbody>
</table>

 

**Int**命令の特殊なケースを次に示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>INT</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>デバッガーのブレークポイントトラップ。</p></td>
</tr>
</tbody>
</table>

 

**INT 3**のオペコードは0xcc です。 **NOP**のオペコードは0x90 です。

コードをデバッグするときに、コードを修正することが必要になる場合があります。 これを行うには、問題のあるバイトを0x90 に置き換えます。

### <a name="span-ididiomsspanspan-ididiomsspanspan-ididiomsspanidioms"></a><span id="Idioms"></span><span id="idioms"></span><span id="IDIOMS"></span>表現

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>XOR</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p><strong>r</strong> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>TEST</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p><strong>R</strong>が0かどうかを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>ADD</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p><strong>R</strong>を1ずつ左にシフトします。</p></td>
</tr>
</tbody>
</table>

 

 

 





