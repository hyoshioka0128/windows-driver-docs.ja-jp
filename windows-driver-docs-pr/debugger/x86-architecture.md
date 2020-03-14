---
title: x86 アーキテクチャ
description: x86 アーキテクチャ
ms.assetid: 42c62647-7c9a-496e-839f-91283db73a29
keywords:
- x86 プロセッサ、アーキテクチャ
- x86 プロセッサ上のレジスタ
- x86 プロセッサ、レジスタ
- x86 プロセッサ、呼び出し規約
- x86 プロセッサ、データ型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7da158a055960451e60d2275f2b26333db1fadc5
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242857"
---
# <a name="x86-architecture"></a>x86 アーキテクチャ


## <span id="ddk_x86_architecture_dbg"></span><span id="DDK_X86_ARCHITECTURE_DBG"></span>


Intel x86 プロセッサでは、複雑な命令セットコンピューター (CISC) アーキテクチャが使用されています。つまり、大量の汎用レジスタではなく、特別な用途のレジスタがいくつか存在します。 また、複雑な特別な命令を優位にすることもできます。

X86 プロセッサは、少なくとも8ビット Intel 8080 プロセッサと比べて、そのようなものをトレースします。 X86 命令セットの多くの問題は、そのプロセッサとの下位互換性 (および Zilog の Z-80 variant) によるものです。

Microsoft Win32 では、 *32 ビットのフラットモード*で x86 プロセッサを使用します。 このドキュメントでは、フラットモードのみに焦点を当てています。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>Register

X86 アーキテクチャは、次の特権のない整数レジスタで構成されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>eax</strong></p></td>
<td align="left"><p>アキュムレータ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ebx</strong></p></td>
<td align="left"><p>基本レジスタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ecx</strong></p></td>
<td align="left"><p>カウンターの登録</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p>データレジスタ-i/o ポートアクセスと算術関数に使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p>ソースインデックスレジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>修飾子</strong></p></td>
<td align="left"><p>コピー先のインデックスレジスタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ebp</strong></p></td>
<td align="left"><p>ベースポインターレジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>esp</strong></p></td>
<td align="left"><p>スタックポインター</p></td>
</tr>
</tbody>
</table>

 

すべての整数レジスタは32ビットです。 ただし、その多くには、16ビットまたは8ビットのサブレジスタがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ax</strong></p></td>
<td align="left"><p><strong>Eax</strong>の下位16ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p><strong>Ebx</strong>の下位16ビット</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シリーズ</strong></p></td>
<td align="left"><p><strong>Ecx</strong>の下位16ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p><strong>Edx</strong>の下位16ビット</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p><strong>Esi</strong>の下位16ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p>下位16ビットの<strong>edi</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p>低16ビットの<strong>ebp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロセッサー</strong></p></td>
<td align="left"><p>低16ビットの<strong>esp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ウムアルクラ</strong></p></td>
<td align="left"><p><strong>Eax</strong>の下位8ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ah</strong></p></td>
<td align="left"><p>高8ビットの<strong>ax</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bl</strong></p></td>
<td align="left"><p><strong>Ebx</strong>の低8ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bh</strong></p></td>
<td align="left"><p>高8ビットの<strong>bx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>付い</strong></p></td>
<td align="left"><p><strong>Ecx</strong>の低8ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ハーフ</strong></p></td>
<td align="left"><p>高8ビットの<strong>cx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dl</strong></p></td>
<td align="left"><p><strong>Edx</strong>の下位8ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dh</strong></p></td>
<td align="left"><p>高8ビットの<strong>dx</strong></p></td>
</tr>
</tbody>
</table>

 

Subregister での操作は、subregister にのみ影響し、サブレジスタの外部にあるパーツは一切影響を及ぼしません。 たとえば、 **ax**レジスタに格納すると、 **eax**レジスタの上位16ビットが変更されずに残ります。

を使用する場合[ **(式の評価)** ](---evaluate-expression-.md)コマンドでは、登録の先頭に "at" 記号 ( **@** ) を付ける必要があります。 たとえば、? **ax**ではなく、 <strong>? @ax</strong>を使用する必要があります。 これにより、デバッガーは、シンボルではなくレジスタとして**ax**を認識します。

ただし、 [**r (レジスタ)** ](r--registers-.md)コマンドでは、(@) は必要ありません。 たとえば、 **r ax = 5**は常に正しく解釈されます。

他の2つのレジスタは、プロセッサの現在の状態にとって重要です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>eip</strong></p></td>
<td align="left"><p>命令ポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>示す</strong></p></td>
<td align="left"><p>flags</p></td>
</tr>
</tbody>
</table>

 

命令ポインターは、実行される命令のアドレスです。

Flags register は、1ビットのフラグのコレクションです。 命令の結果を記述するために、多くの命令によってフラグが変更されます。 これらのフラグは、条件付きジャンプ命令によってテストできます。 詳細については、「 [X86 フラグ](#x86-flags)」を参照してください。

### <a name="span-idcalling_conventionsspanspan-idcalling_conventionsspanspan-idcalling_conventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>呼び出し規約

X86 アーキテクチャには、いくつかの異なる呼び出し規約があります。 幸いにも、これらはすべて同じレジスタの保存と関数の戻り値に従います。

-   関数は、 **eax**、 **ecx**、および**edx**を除くすべてのレジスタを保持する必要があります。これは関数呼び出しで変更でき、 **esp**は呼び出し規約に従って更新する必要があります。

-   結果が32ビット以下の場合、 **eax**レジスタは関数の戻り値を受け取ります。 結果が64ビットの場合、結果は**edx: eax**ペアに格納されます。

X86 アーキテクチャで使用される呼び出し規則の一覧を次に示します。

-   Win32 ( **\_\_stdcall**)

    関数のパラメーターはスタックで渡され、右から左にプッシュされ、呼び出し先がスタックを消去します。

-   ネイティブC++メソッド呼び出し (thiscall とも呼ばれます)

    関数のパラメーターはスタックで渡され、右から左にプッシュされ、"this" ポインターが**ecx**レジスタに渡され、呼び出し先がスタックを消去します。

-   COM (メソッド呼び出しのC++ **\_\_stdcall** )

    関数のパラメーターはスタックで渡され、右から左にプッシュされた後、"this" ポインターがスタックにプッシュされた後、関数が呼び出されます。 呼び出し先がスタックを消去します。

-   **\_\_fastcall**

    最初の2つの DWORD または小さい引数は、 **ecx**および**edx**レジスタに渡されます。 残りのパラメーターはスタックで渡され、右から左にプッシュされます。 呼び出し先がスタックを消去します。

-   **\_\_cdecl**

    関数のパラメーターはスタックで渡され、右から左にプッシュされ、呼び出し元がスタックを消去します。 **\_\_cdecl**呼び出し規約は、可変長パラメーターを持つすべての関数に使用されます。

### <a name="span-iddebugger_display_of_registers_and_flagsspanspan-iddebugger_display_of_registers_and_flagsspanspan-iddebugger_display_of_registers_and_flagsspandebugger-display-of-registers-and-flags"></a><span id="Debugger_Display_of_Registers_and_Flags"></span><span id="debugger_display_of_registers_and_flags"></span><span id="DEBUGGER_DISPLAY_OF_REGISTERS_AND_FLAGS"></span>レジスタとフラグのデバッガー表示

デバッガーレジスタの表示の例を次に示します。

```dbgcmd
eax=00000000 ebx=008b6f00 ecx=01010101 edx=ffffffff esi=00000000 edi=00465000
eip=77f9d022 esp=05cffc48 ebp=05cffc54 iopl=0         nv up ei ng nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000286
```

ユーザーモードのデバッグでは、 **iopl**と、デバッガー表示の最後の行全体を無視できます。

### <a name="span-idx86-flagsspanspan-idx86_flagsspanx86-flags"></a><span id="x86-flags"></span><span id="X86_FLAGS"></span>x86 フラグ

前の例では、2行目の末尾にある2文字のコードが*フラグ*です。 これらはシングルビットレジスタで、さまざまな用途があります。

次の表に、x86 フラグの一覧を示します。

フラグコードフラグ名値フラグステータスステータス**の**説明

オーバーフローフラグ

0 1 **nvov**

オーバーフローオーバーフロー **df**なし

方向フラグ

0 1 **updn**

**If**の方向方向

割り込みフラグ

0 1 **diei**

無効な割り込みが有効になっている**sf**

符号フラグ

0 1 **plng**

正 (またはゼロ) のマイナス**zf**

ゼロフラグ

0 1 **nzzr**

0以外の**af**

補助キャリーフラグ

0 1 **naac**

補助キャリーのキャリー **pf**がありません

パリティフラグ

0 1 **pepo**

パリティ**偶数パリティ (奇数)**

キャリーフラグ

0 1 **nccy**

キャリー**を受けて**いません

トラップフラグ

**Tf**が1に等しい場合、プロセッサは1つの命令の実行後に1つの\_ステップの例外\_状態を生成します。 このフラグは、シングルステップのトレースを実装するためにデバッガーによって使用されます。 他のアプリケーションでは使用できません。

**iopl**

I/o 特権レベル

これは、0 ~ 3 の値を持つ2ビット整数です。 これは、ハードウェアへのアクセスを制御するためにオペレーティングシステムによって使用されます。 アプリケーションでは使用しないでください。

 

デバッガーコマンドウィンドウの一部のコマンドの結果としてレジスタが表示される場合は、表示されている*フラグの状態*になります。 ただし、 [**r (レジスタ)** ](r--registers-.md)コマンドを使用してフラグを変更する場合は、*フラグコード*でそれを参照する必要があります。

WinDbg の [レジスタ] ウィンドウでは、フラグコードを使用してフラグを表示または変更します。 フラグの状態はサポートされていません。

次に例を示します。 上記のレジスタ表示には、フラグステータス**ng**が表示されます。 これは、符号フラグが現在1に設定されていることを意味します。 これを変更するには、次のコマンドを使用します。

```dbgcmd
r sf=0
```

これにより、符号フラグが0に設定されます。 別の登録を表示した場合、 **ng**ステータスコードは表示されません。 代わりに、 **pl**ステータスコードが表示されます。

Sign フラグ、0フラグ、およびキャリーフラグは、最も一般的に使用されるフラグです。

### <a name="span-idconditionsspanspan-idconditionsspanspan-idconditionsspanconditions"></a><span id="Conditions"></span><span id="conditions"></span><span id="CONDITIONS"></span>照明

*条件*は、1つまたは複数のフラグの状態を表します。 X86 でのすべての条件付き操作は、条件に基づいて表現されます。

アセンブラーは、1文字または2文字の省略形を使用して条件を表します。 条件は、複数の省略形で表すことができます。 たとえば、AE ("上または等しい") は、NB と同じ条件です ("次の値ではありません")。 次の表に、一般的な条件とその意味を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件名</th>
<th align="left">フラグ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Z</p></td>
<td align="left"><p>ZF = 1</p></td>
<td align="left"><p>最後の操作の結果が0でした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NZ</p></td>
<td align="left"><p>ZF = 0</p></td>
<td align="left"><p>最後の操作の結果が0ではありませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p>最後の操作には、キャリーまたは借りるが必要です。 符号なし整数の場合は、オーバーフローを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>加工</p></td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p>最後の操作では、キャリーまたは借りるは必要ありませんでした。 符号なし整数の場合は、オーバーフローを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>SF = 1</p></td>
<td align="left"><p>最後の操作の結果には、上位ビットが設定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS</p></td>
<td align="left"><p>SF = 0</p></td>
<td align="left"><p>最後の操作の結果は、高いビットクリアになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>O</p></td>
<td align="left"><p>= 1</p></td>
<td align="left"><p>符号付き整数演算として処理された場合、最後の操作でオーバーフローまたはアンダーフローが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用不可</p></td>
<td align="left"><p>= 0</p></td>
<td align="left"><p>符号付き整数演算として処理された場合、最後の操作でオーバーフローまたはアンダーフローは発生しませんでした。</p></td>
</tr>
</tbody>
</table>

 

条件を使用して、2つの値を比較することもできます。 **Cmp**命令は、2つのオペランドを比較し、一方のオペランドをもう一方のオペランドから減算した場合と同様にフラグを設定します。 次の条件を使用して、 **cmp** *value1*, *value2*の結果を確認できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件名</th>
<th align="left">フラグ</th>
<th align="left">CMP 操作後の意味です。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>ZF = 1</p></td>
<td align="left"><p><em>value1</em> == <em>value2</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NE</p></td>
<td align="left"><p>ZF = 0</p></td>
<td align="left"><p><em>value1</em> ! = <em>value2</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
GE NL</td>
<td align="left"><p>SF = OF</p></td>
<td align="left"><p></p>
<em>value1</em> &gt;= <em>value2</em>です。
値は符号付き整数として扱われます。</td>
</tr>
<tr class="even">
<td align="left"><p></p>
LE NG</td>
<td align="left"><p>ZF = 1 または SF! = OF</p></td>
<td align="left"><p><em>value1</em> &lt;= <em>value2</em>です。 値は符号付き整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
G NLE</td>
<td align="left"><p>ZF = 0 および SF = OF</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>。 値は符号付き整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
L NGE</td>
<td align="left"><p>SF! = OF</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>。 値は符号付き整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
AE NB</td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p><em>value1</em> &gt;= <em>value2</em>です。 値は符号なし整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
NA</td>
<td align="left"><p>CF = 1 または ZF = 1</p></td>
<td align="left"><p><em>value1</em> &lt;= <em>value2</em>です。 値は符号なし整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
NBE</td>
<td align="left"><p>CF = 0 および ZF = 0</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>。 値は符号なし整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
B NAE</td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>。 値は符号なし整数として扱われます。</p></td>
</tr>
</tbody>
</table>

 

通常、条件は、 **cmp**または**テスト**命令の結果を操作するために使用されます。 以下に例を示します。

```asm
cmp eax, 5
jz equal
```

式 (**eax** -5) を計算し、結果に従ってフラグを設定することによって、 **eax**レジスタを数値5と比較します。 減算の結果が0の場合は、 **zr**フラグが設定され、 **jz**条件は true になり、ジャンプが実行されます。

### <a name="span-iddata_typesspanspan-iddata_typesspanspan-iddata_typesspandata-types"></a><span id="Data_Types"></span><span id="data_types"></span><span id="DATA_TYPES"></span>データ型

-   byte: 8 ビット

-   word:16 ビット

-   dword:32 ビット

-   qword:64 ビット (浮動小数点 double を含む)

-   tword:80 ビット (浮動小数点拡張 double を含む)

-   oword: 128 ビット

### <a name="span-idnotationspanspan-idnotationspanspan-idnotationspannotation"></a><span id="Notation"></span><span id="notation"></span><span id="NOTATION"></span>表し

次の表は、アセンブリ言語の手順を説明するために使用される表記法を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表し</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>r</strong>、 <strong>r1</strong>、 <strong>r2</strong>...</p></td>
<td align="left"><p>レジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>メモリアドレス (詳細については、「次のアドレス指定モード」を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#n</p></td>
<td align="left"><p>イミディエイト定数</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>レジスタまたはメモリ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r</strong>/#n</p></td>
<td align="left"><p>Register または immediate 定数</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>Register、memory、または immediate 定数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>問い合わせ</em></p></td>
<td align="left"><p>前の条件セクションに一覧表示されている条件コード。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>\T</em></p></td>
<td align="left"><p>"B"、"W"、"D" (バイト、単語、または dword)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>acc<em>T</em></p></td>
<td align="left"><p>Size <em>t</em>アキュムレータ: <strong>al</strong> If <em>t</em> = "B"、 <strong>ax</strong> if <em>t</em> = "W"、または<strong>eax</strong> if <em>t</em> = "D"</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaddressing_modesspanspan-idaddressing_modesspanspan-idaddressing_modesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>アドレス指定モード

アドレス指定モードはいくつかありますが、すべての形式は**t ptr \[expr\]** になります。ここで、 **t**は一部のデータ型で、 **expr**は定数とレジスタを含む式です。

ほとんどのモードの表記は、かなり難しいことなく推測できます。 たとえば、**バイト PTR \[esi + edx\*8 + 3\]** は、" **esi**レジスタの値を取得し、 **edx**レジスタの値の8倍に追加し、3を加算した後、結果のアドレスのバイトにアクセスすることを意味します。"

### <a name="span-idpipeliningspanspan-idpipeliningspanspan-idpipeliningspanpipelining"></a><span id="Pipelining"></span><span id="pipelining"></span><span id="PIPELINING"></span>処理

Pentium はデュアル問題です。つまり、1つのクロック目盛りで最大2つのアクションを実行できます。 ただし、2つのアクション (*ペアリング*と呼ばれます) を同時に実行できる場合の規則は非常に複雑です。

X86 は CISC プロセッサであるため、ジャンプ遅延スロットについて心配する必要はありません。

### <a name="span-idsynchronized_memory_accessspanspan-idsynchronized_memory_accessspanspan-idsynchronized_memory_accessspansynchronized-memory-access"></a><span id="Synchronized_Memory_Access"></span><span id="synchronized_memory_access"></span><span id="SYNCHRONIZED_MEMORY_ACCESS"></span>同期されたメモリアクセス

読み込み、変更、および格納の命令は、次のように命令を変更する**ロック**プレフィックスを受け取ることができます。

1.  命令を発行する前に、CPU はすべての保留中のメモリ操作をフラッシュして一貫性を確保します。 すべてのデータプリフェッチが破棄されます。

2.  命令の発行時に、CPU はバスに排他的にアクセスできます。 これにより、読み込み/変更/ストア操作の原子性が確保されます。

**Xchg**命令は、メモリで値を交換するたびに、前の規則に自動的に従います。

その他のすべての命令は、既定で非ロックに設定されます。

### <a name="span-idjump_predictionspanspan-idjump_predictionspanspan-idjump_predictionspanjump-prediction"></a><span id="Jump_Prediction"></span><span id="jump_prediction"></span><span id="JUMP_PREDICTION"></span>ジャンプ予測

無条件のジャンプは予想されます。

条件付きジャンプは、前回の実行時に取得されたかどうかによって、取得されるかどうかが予測されます。 ジャンプ履歴を記録するためのキャッシュのサイズは制限されています。

条件付きジャンプが実行されたかどうか、または前回の実行時に取得されていないことを示す記録が CPU にない場合は、前の条件付きジャンプが実行されたと予測され、条件付きジャンプは実行されません。

### <a name="span-idalignmentspanspan-idalignmentspanspan-idalignmentspanalignment"></a><span id="Alignment"></span><span id="alignment"></span><span id="ALIGNMENT"></span>配置

X86 プロセッサは、パフォーマンスが低下したときに、自動的に整列されていないメモリアクセスを修正します。 例外は発生しません。

アドレスがオブジェクトサイズの倍数の整数である場合、メモリアクセスはアラインされたと見なされます。 たとえば、すべてのバイトアクセスがアラインされている (すべてが1の整数の倍数)、WORD による偶数のアドレスへのアクセスがアラインされ、DWORD アドレスは4の倍数である必要があります。

固定されていないメモリアクセスには、**ロック**プレフィックスを使用しないでください。

 

 





