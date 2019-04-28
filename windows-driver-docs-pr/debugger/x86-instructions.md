---
title: x86 の手順
description: x86 の手順
ms.assetid: 237796d5-ef82-4eab-8d56-3191b3e63597
keywords:
- x86 プロセッサで命令
- x86 プロセッサでは、算術演算
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2310fd4e39c0c1072df7099c58c35bdc808cf2be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381895"
---
# <a name="x86-instructions"></a>x86 の手順


## <span id="ddk_x86_instructions_dbg"></span><span id="DDK_X86_INSTRUCTIONS_DBG"></span>


このセクションの一覧を手順はアスタリスクが付いた (* *\\* * *) は特に重要です。 そうでもないマークされている手順は重要ではないです。

X86 プロセッサでは、手順については、可変サイズ、パターン マッチングの課題は、逆方向を逆アセンブルためです。 アドレスから逆方向を逆アセンブルするには、戻す、移動し、手順については、合理的に開始されるまで、楽しみたいよりもさらで逆アセンブルを開始する必要があります。 最初の手順については、いくつかが起動する命令の途中で逆アセンブルした可能性がありますので意味が、ありません。 可能性がある、残念ながら、逆アセンブルが命令ストリームを同期させることはありませんし、動作する開始点が見つかるまで、さまざまな開始位置に逆アセンブルする必要があります。

適切なパックされた**スイッチ**ステートメント、コンパイラは、生成データ、コード ストリームに直接これを逆アセンブル、**切り替える**ステートメントは通常 1 つ 1 つ、意味 (手順いるため、実際にデータ)。 データの末尾を見つけて、逆アセンブルを続行します。

### <a name="span-idinstructionnotationspanspan-idinstructionnotationspanspan-idinstructionnotationspaninstruction-notation"></a><span id="Instruction_Notation"></span><span id="instruction_notation"></span><span id="INSTRUCTION_NOTATION"></span>命令の表記

手順については、一般的な表記は、左側と右側のソース、宛先レジスタを置くことです。 ただし、このルールをいくつかの例外があります。

算術命令は通常 2 つの登録をソースとし、変換先は、結合を登録します。 結果は、変換先に格納されます。

16 ビットと 32 ビットの両方のバージョンがある一部の手順が、32 ビット バージョンのみを紹介します。 一覧にないは、浮動小数点命令、特権のある手順については、および手順については、(これは、Microsoft Win32 を使用しません)、セグメント化されたモデルでのみ使用されます。

容量を節約するには、手順の多くで表現されます結合されたフォームは、次の例に示すようにします。

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
<td align="left"><p><strong>r1</strong> = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

最初のパラメーターはレジスタである必要がありますが、2 つ目は、レジスタ、メモリの参照、またはイミディ エイト値をことを意味します。

さらに多くの容量を節約するには、手順についても表現できますでは、次に示すようにします。

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

 

つまり最初のパラメーターはレジスタまたはメモリの参照と、2 つ目は、レジスタ、メモリ参照が、またはイミディ エイト値を指定できます。

明記されない限り、この省略形を使用する場合、ソースと宛先の両方のメモリを選択することはできません。

さらに、ソースまたは変換先を示すパラメーターは、そのサイズのある必要があります (8、16、32) のビット サイズ サフィックスを追加できます。 たとえば、r8、8 ビット レジスタを意味します。

### <a name="span-idmemorydatatransferanddataconversionspanspan-idmemorydatatransferanddataconversionspanspan-idmemorydatatransferanddataconversionspanmemory-data-transfer-and-data-conversion"></a><span id="Memory__Data_Transfer__and_Data_Conversion"></span><span id="memory__data_transfer__and_data_conversion"></span><span id="MEMORY__DATA_TRANSFER__AND_DATA_CONVERSION"></span>メモリ、データ転送、およびデータ変換

メモリとデータ転送命令では、フラグは影響しません。

### <a name="span-ideffectiveaddressspanspan-ideffectiveaddressspanspan-ideffectiveaddressspaneffective-address"></a><span id="Effective_Address"></span><span id="effective_address"></span><span id="EFFECTIVE_ADDRESS"></span>有効なアドレス

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
<td align="left"><p>元に戻せる</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p>有効なアドレスをロードします。</p>
<p>(r = m のアドレス)</p></td>
</tr>
</tbody>
</table>

 

たとえば、**元に戻せる eax、 \[esi + 4\]** 意味**eax** = **esi** + 4。 この命令は、算術演算を実行するよく使用されます。

### <a name="span-iddatatransferspanspan-iddatatransferspanspan-iddatatransferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>データ転送

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
<td align="left"><p>符号拡張と共に移動します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOVZX</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>0 個の拡張機能と共に移動します。</p></td>
</tr>
</tbody>
</table>

 

**MOVSX**と**MOVZX**の特別なバージョンは、 **mov**先に元の符号拡張、または 0 個の拡張機能を実行する命令です。 これは、移行元と変換先を異なるサイズを設定できる唯一の命令です。 (また、実際には、さまざまなサイズがあります。

### <a name="span-idstackmanipulationspanspan-idstackmanipulationspanspan-idstackmanipulationspanstack-manipulation"></a><span id="Stack_Manipulation"></span><span id="stack_manipulation"></span><span id="STACK_MANIPULATION"></span>スタック操作

指すは、スタック、 **esp**を登録します。 ある値**esp** (最近、最初にプッシュ ポップされます)。 スタックの一番上には古いスタック要素は、上位アドレスに存在します。

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
<td align="left"><p>プッシュ</p></td>
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>値をスタックにプッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>POP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>値をスタックからポップします。</p></td>
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
<td align="left"><p>スタックからポップ フラグ。</p></td>
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
<td align="left"><p>#n, #n</p></td>
<td align="left"><p>スタック フレームを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>ままにしてください。</p></td>
<td align="left"></td>
<td align="left"><p>スタック フレームを破棄します。</p></td>
</tr>
</tbody>
</table>

 

C と C++ コンパイラが使用しない、**入力**命令。 (、**入力**Algol や Pascal などの言語で入れ子になったプロシージャを実装する命令を使用します)。

**まま**命令は等価です。

```asm
mov esp, ebp
pop ebp
```

### <a name="span-iddataconversionspanspan-iddataconversionspanspan-iddataconversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>データ変換

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CBW</p></td>
<td align="left"><p>バイトに変換 (<strong>al</strong>) word (<strong>ax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CWD</p></td>
<td align="left"><p>Word の変換 (<strong>ax</strong>) を dword (<strong>dx</strong>:<strong>ax</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CWDE</p></td>
<td align="left"><p>Word の変換 (<strong>ax</strong>) を dword (<strong>eax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CDQ</p></td>
<td align="left"><p>dword を変換 (<strong>eax</strong>) には、qword (<strong>edx</strong>:<strong>eax</strong>)。</p></td>
</tr>
</tbody>
</table>

 

すべての変換では、符号拡張を実行します。

### <a name="span-idarithmeticandbitmanipulationspanspan-idarithmeticandbitmanipulationspanspan-idarithmeticandbitmanipulationspanarithmetic-and-bit-manipulation"></a><span id="Arithmetic_and_Bit_Manipulation"></span><span id="arithmetic_and_bit_manipulation"></span><span id="ARITHMETIC_AND_BIT_MANIPULATION"></span>算術演算子およびビット操作

すべての算術演算子とビット操作命令では、フラグを変更します。

### <a name="span-idarithmeticspanspan-idarithmeticspanspan-idarithmeticspanarithmetic"></a><span id="Arithmetic"></span><span id="arithmetic"></span><span id="ARITHMETIC"></span>算術演算子

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
<td align="left"><p><strong>r1</strong>/m += <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>ADC</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r2</strong>/m/#n + 実行</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SUB</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>SBB</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n + 実行</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>NEG</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m = -<strong>r1</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>INC</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m += 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>12 月</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m -= 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CMP</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>コンピューティング<strong>r1</strong>/m - <strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**Cmp**命令を減算し、結果では、フラグを設定しますが、すぐに結果をスローします。 条件文に続く通常**ジャンプ**減算の結果をテストする命令です。

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
<td align="left"><p><strong>r1</strong> *= <strong>r2</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、#n</p></td>
<td align="left"><p><strong>r1</strong> = <strong>r2</strong>/m * #n</p></td>
</tr>
</tbody>
</table>

 

符号なしと署名済みの乗算します。 乗算の後のフラグの状態は定義されません。

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
<td align="left"><p>(<strong>edx</strong>、 <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
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
<td align="left"><p>(<strong>edx</strong>、 <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
</tr>
</tbody>
</table>

 

符号なしと署名済みの除算します。 擬似コードについては、最初の登録は、残りの部分を受け取り、2 つ目の商を受信します。 結果はオーバーフロー、変換先、除算のオーバーフロー例外が生成されます。

除算の後のフラグの状態は定義されません。

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
<td align="left"><p>設定<em>cc</em></p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>設定<strong>r</strong>/m8 を 0 または 1</p></td>
</tr>
</tbody>
</table>

 

場合、条件*cc*が true の場合、8 ビット値が 1 に設定します。 それ以外の場合、8 ビット値は 0 に設定されます。

### <a name="span-idbinary-codeddecimalspanspan-idbinary-codeddecimalspanspan-idbinary-codeddecimalspanbinary-coded-decimal"></a><span id="Binary-coded_Decimal"></span><span id="binary-coded_decimal"></span><span id="BINARY-CODED_DECIMAL"></span>バイナリ コード化された 10 進数

COBOL で記述されたコードをデバッグしていない場合に、次の手順を表示はされません。

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
<td align="left"><p>追加後に 10 進数を調整します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>DAS</p></td>
<td align="left"><p>減算後 10 進数を調整します。</p></td>
</tr>
</tbody>
</table>

 

これらの手順の調整、 **al**パックされたバイナリ コード化された 10 進操作の実行後に登録します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAA</p></td>
<td align="left"><p>ASCII は、追加した後に調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAS</p></td>
<td align="left"><p>ASCII は、減算した後に調整します。</p></td>
</tr>
</tbody>
</table>

 

これらの手順の調整、 **al**アンパックされたバイナリ コード化された 10 進操作の実行後に登録します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAM</p></td>
<td align="left"><p>ASCII は、乗算の後に調整します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAD</p></td>
<td align="left"><p>ASCII は、除算した後に調整します。</p></td>
</tr>
</tbody>
</table>

 

これらの手順の調整、 **al**と**ah**アンパック バイナリ-コード化された 10 進数の操作を実行した後に登録します。

### <a name="span-idbitsspanspan-idbitsspanspan-idbitsspanbits"></a><span id="Bits"></span><span id="bits"></span><span id="BITS"></span>Bits

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
<td align="left"><p>および</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m と<strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>または</p></td>
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
<td align="left"><p><strong>r1</strong>/m = ビットごと<strong>r1</strong>/m</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>テスト</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>コンピューティング<strong>r1</strong>/m と<strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**テスト**命令論理 AND 演算子を計算し、結果では、フラグを設定しますが、すぐに結果をスローします。 論理 AND の結果をテストする条件付きのジャンプ命令に続く通常

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
<td align="left"><p><strong>r1</strong>/m &lt;&lt;= <strong>cl</strong>/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SHR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; &gt; =  <strong>cl</strong>/#n 0 埋め</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>SAR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; &gt; =  <strong>cl</strong>/#n 記号の塗りつぶし</p></td>
</tr>
</tbody>
</table>

 

最後のビットをシフトは、キャリーに配置されます。

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
<td align="left"><p>左ダブルをシフトします。</p></td>
</tr>
</tbody>
</table>

 

Shift キーを押し**r1**で左**cl**/\#の最上位ビットに n **r2**/m します。 最後のビットをシフトは、キャリーに配置されます。

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
<td align="left"><p>倍精度浮動小数点右側にシフトします。</p></td>
</tr>
</tbody>
</table>

 

Shift キーを押し**r1**右**cl**/\#の下位ビットに n **r2**/m。 最後のビットをシフトは、キャリーに配置されます。

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
<td align="left"><p>回転<strong>r1</strong>で左<strong>cl</strong>/#n します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>権限が必要です。</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>回転<strong>r1</strong>右<strong>cl</strong>/#n します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RCL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>回転<strong>r1</strong>/C 左<strong>cl</strong>/#n します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RCR</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>回転<strong>r1</strong>/C 右<strong>cl</strong>/#n します。</p></td>
</tr>
</tbody>
</table>

 

回転は、受信の塗りつぶしのビットをシフトするビットが再び表示する点を除いて、シフトなどです。 回転の命令の C 言語のバージョンでは、回転に実行ビットを組み込みます。

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
<td align="left"><p>コピー ビット<strong>r2</strong>の/#n <strong>r1</strong>キャリーにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BTS</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p>設定されたビット<strong>r2</strong>の/#n <strong>r1</strong>キャリーに前の値をコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BTC</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p>クリア ビット<strong>r2</strong>の/#n <strong>r1</strong>キャリーに前の値をコピーします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrolflowspanspan-idcontrolflowspanspan-idcontrolflowspancontrol-flow"></a><span id="Control_Flow"></span><span id="control_flow"></span><span id="CONTROL_FLOW"></span>制御フロー

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
<td align="left"><p>追加先</p></td>
<td align="left"><p>条件付き分岐します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p>追加先</p></td>
<td align="left"><p>直接ジャンプします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>間接的なジャンプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p>追加先</p></td>
<td align="left"><p>直接呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>間接的な呼び出しです。</p></td>
</tr>
</tbody>
</table>

 

**呼び出す**命令は、戻り値のアドレスがスタックにプッシュし、先にジャンプします。

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
<td align="left"><p><em>#n</em></p></td>
<td align="left"><p>戻り値</p></td>
</tr>
</tbody>
</table>

 

**Ret**命令をポップし、スタックの戻り値のアドレスにジャンプします。 0 以外の場合、  *\#n*で、 **RET**命令が戻り値のアドレス値をポップアップ表示後に示す *\#n*スタックに追加する必要がありますポインター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ループ</p></td>
<td align="left"><p>デクリメント<strong>ecx</strong>と結果が 0 以外の場合にジャンプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LOOPZ</p></td>
<td align="left"><p>デクリメント<strong>ecx</strong>ジャンプする結果が 0 以外の場合と<strong>zr</strong>設定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LOOPNZ</p></td>
<td align="left"><p>デクリメント<strong>ecx</strong>ジャンプする結果が 0 以外の場合と<strong>zr</strong>は明らかでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>JECXZ</p></td>
<td align="left"><p>場合のジャンプ<strong>ecx</strong>は 0 です。</p></td>
</tr>
</tbody>
</table>

 

これらの手順は、最新のプロセッサで、x86 の CISC 遺産のゴミが長い方法を記述された同等の命令よりも実質的に遅くなります。

### <a name="span-idstringmanipulationspanspan-idstringmanipulationspanspan-idstringmanipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>文字列操作

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
<td align="left"><p>移動<em>T</em>から<strong>esi</strong>に<strong>edi です。</strong></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>CMPS<em>T</em></p></td>
<td align="left"><p>比較<em>T</em>から<strong>esi</strong>で<strong>edi です。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SCA<em>T</em></p></td>
<td align="left"><p>スキャン<em>T</em>から<strong>edi</strong> acc の<em>t です。</em></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>LOD<em>T</em></p></td>
<td align="left"><p>ロード<em>T</em>から<strong>esi</strong> acc に<em>t です。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>STOS<em>T</em></p></td>
<td align="left"><p>ストア<em>T</em>に<strong>edi</strong> acc から<em>t です。</em></p></td>
</tr>
</tbody>
</table>

 

操作を実行した後、ソースと宛先レジスタはインクリメントまたはデクリメント sizeof によって (*T*)、方向フラグ (上下) の設定に従ってします。

命令の先頭**REP**によって指定された時間数の操作を繰り返します、 **ecx**を登録します。

**Rep mov**命令を使用してメモリのブロックをコピーします。

**Rep stos**命令を使用してメモリ ブロックをアクセスで塗りつぶす*T*します。

### <a name="span-idflagsspanspan-idflagsspanspan-idflagsspanflags"></a><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>フラグ

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>LAHF</p></td>
<td align="left"><p>ロード<strong>ah</strong>フラグから。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SAHF</p></td>
<td align="left"><p>ストア<strong>ah</strong>フラグ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STC</p></td>
<td align="left"><p>実行を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLC</p></td>
<td align="left"><p>チェック ボックスをオフに設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMC</p></td>
<td align="left"><p>キャリーを補完します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STD</p></td>
<td align="left"><p>方向を設定<em>ダウンします。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLD</p></td>
<td align="left"><p>方向を設定<em>をします。</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>STI</p></td>
<td align="left"><p>割り込みを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLI (CLI)</p></td>
<td align="left"><p>割り込みを無効にします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinterlockedinstructionsspanspan-idinterlockedinstructionsspanspan-idinterlockedinstructionsspaninterlocked-instructions"></a><span id="Interlocked_Instructions"></span><span id="interlocked_instructions"></span><span id="INTERLOCKED_INSTRUCTIONS"></span>インタロックされた手順

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
<td align="left"><p>スワップ<strong>r1</strong>と<strong>r</strong>/m します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XADD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>追加<strong>r1</strong>に<strong>r</strong>、m に元の値を格納/<strong>r1。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMPXCHG</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>比較および交換条件。</p></td>
</tr>
</tbody>
</table>

 

**Cmpxchg**命令は、次のアトミック バージョン。

```asm
   cmp     accT, r/m
   jz      match
   mov     accT, r/m
   jmp     done
match:
   mov     r/m, r1
done:
```

### <a name="span-idmiscellaneousspanspan-idmiscellaneousspanspan-idmiscellaneousspanmiscellaneous"></a><span id="Miscellaneous"></span><span id="miscellaneous"></span><span id="MISCELLANEOUS"></span>その他

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
<td align="left"><p>#n</p></td>
<td align="left"><p>カーネルをトラップします。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>バインドされています。</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p>場合のトラップ<strong>r</strong>範囲内にありません。</p></td>
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
<td align="left"><p>レジスタにバイト順をスワップします。</p></td>
</tr>
</tbody>
</table>

 

ここでは、特殊なケース、 **int**命令。

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
<td align="left"><p>デバッガーのブレークポイントのトラップ。</p></td>
</tr>
</tbody>
</table>

 

オペコード**INT 3** 0 xcc です。 オペコード**NOP** 0x90 します。

コードをデバッグするときは、いくつかのコードを修正プログラムを適用する必要があります。 0x90 に問題が発生したバイトを置き換えることにより、これを行うことができます。

### <a name="span-ididiomsspanspan-ididiomsspanspan-ididiomsspanidioms"></a><span id="Idioms"></span><span id="idioms"></span><span id="IDIOMS"></span>表現方法

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
<td align="left"><p>テスト</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p>場合確認<strong>r</strong> = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>ADD</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p>Shift キーを押し<strong>r</strong>を 1 つのままです。</p></td>
</tr>
</tbody>
</table>

 

 

 





