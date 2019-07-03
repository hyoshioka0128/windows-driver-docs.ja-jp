---
title: x86 アーキテクチャ
description: x86 アーキテクチャ
ms.assetid: 42c62647-7c9a-496e-839f-91283db73a29
keywords:
- x86 プロセッサ、アーキテクチャ
- レジスタ、x86 プロセッサ
- x86 プロセッサを登録します
- x86 プロセッサ、呼び出し規則
- x86 プロセッサ、データ型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7da158a055960451e60d2275f2b26333db1fadc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381914"
---
# <a name="x86-architecture"></a>x86 アーキテクチャ


## <span id="ddk_x86_architecture_dbg"></span><span id="DDK_X86_ARCHITECTURE_DBG"></span>


Intel x86 プロセッサでは、大量の汎用レジスタではなく、専用のレジスタの適度な数があることを意味する複雑な命令セット コンピューター (CISC) アーキテクチャを使用します。 また、複雑な手順については特別な用途は predominate することも意味します。

X86 プロセッサでは、その遺産を少なくともトレースは、8 ビット intel 8080 プロセッサをバックアップします。 多くの特殊命令セットがそのプロセッサ (とその新た Z-80 バリアントで) は、旧バージョンとの互換性のためには、x86。

使用して x86 プロセッサを Microsoft Win32 *32 ビット フラット モード*します。 このドキュメントでは、フラット モードのみ焦点を当てます。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>レジスタ

X86 アーキテクチャは、次の特権のない整数で構成されますが登録されます。

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
<td align="left"><p>登録を基本します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ecx</strong></p></td>
<td align="left"><p>カウンターの登録</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p>データ レジスタが使用できる I/O ポートへのアクセスおよび算術関数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p>ソース インデックス レジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edi</strong></p></td>
<td align="left"><p>ターゲット インデックス レジスタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ebp</strong></p></td>
<td align="left"><p>基本ポインター レジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>esp</strong></p></td>
<td align="left"><p>スタック ポインター</p></td>
</tr>
</tbody>
</table>

 

すべての整数レジスタは、32 ビットです。 ただし、それらの多くは 16 ビットまたは 8 ビット subregisters があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Ax</strong></p></td>
<td align="left"><p>16 ビットを低<strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p>16 ビットを低<strong>ebx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cx</strong></p></td>
<td align="left"><p>16 ビットを低<strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p>16 ビットを低<strong>edx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p>16 ビットを低<strong>esi</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p>16 ビットを低<strong>edi</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p>16 ビットを低<strong>ebp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sp</strong></p></td>
<td align="left"><p>16 ビットを低<strong>esp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Al</strong></p></td>
<td align="left"><p>8 ビットの低<strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ah</strong></p></td>
<td align="left"><p>上位の 8 ビット<strong>ax</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bl</strong></p></td>
<td align="left"><p>8 ビットの低<strong>ebx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bh</strong></p></td>
<td align="left"><p>上位の 8 ビット<strong>bx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cl</strong></p></td>
<td align="left"><p>8 ビットの低<strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ch</strong></p></td>
<td align="left"><p>上位の 8 ビット<strong>cx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dl</strong></p></td>
<td align="left"><p>8 ビットの低<strong>edx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dh</strong></p></td>
<td align="left"><p>上位の 8 ビット<strong>dx</strong></p></td>
</tr>
</tbody>
</table>

 

Subregister のみと、subregister の外側の部分のいずれも、subregister で動作に影響します。 格納するなど、 **ax**レジスタの上位 16 ビットのまま、 **eax**変更なしに登録します。

使用する場合、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)コマンド、レジスタは"at"記号を付ける必要があります ( **@** )。 たとえば、使用する必要があります<strong>でしょうか。@ax</strong> なく **? ax**します。 これにより、デバッガーが認識している**ax**シンボルではなくレジスタとして。

ただし、(@) では必要ありません、 [ **r (レジスタ)** ](r--registers-.md)コマンド。 たとえば、 **r ax = 5**常に正しく解釈されます。

その他の 2 つのレジスタは、プロセッサの現在の状態に対して重要です。

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
<td align="left"><p><strong>flags</strong></p></td>
<td align="left"><p>flags</p></td>
</tr>
</tbody>
</table>

 

命令ポインターは、実行されている命令のアドレスです。

フラグ レジスタは、単一のビット フラグのコレクションです。 多くの命令では、命令の結果を示すフラグを変更します。 これらのフラグは、条件付きのジャンプ先の手順でテストできます。 参照してください[x86 フラグ](#x86-flags)詳細についてはします。

### <a name="span-idcallingconventionsspanspan-idcallingconventionsspanspan-idcallingconventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>呼び出し規則

X86 アーキテクチャにいくつかの異なる呼び出し規則があります。 さいわい、これらはすべてエラーは、同じのレジスタ保存および関数の戻り値の規則に従います。

-   関数は、以外のすべてのレジスタを保持する必要が**eax**、 **ecx**、および**edx**、関数の呼び出しの間で変更できますと**esp**、これは、呼び出し規則に従って更新する必要があります。

-   **Eax**結果が 32 ビットの場合、レジスタが関数の戻り値を受け取るまたは小さくします。 結果は 64 ビット、しで結果が格納されているかどうか、 **edx:eax**ペア。

呼び出し、x86 上で使用される規則の一覧を次にアーキテクチャ。

-   Win32 ( **\_\_stdcall**)

    関数のパラメーターは、左、右プッシュ、スタックに渡され、呼び出し先がスタックを消去します。

-   ネイティブ C++ メソッドの呼び出し (thiscall とも呼ばれます)

    関数のパラメーターは、左に右プッシュ、スタックに渡される、"this"ポインターが渡された、 **ecx**レジスタ、および呼び出し先がスタックを消去します。

-   COM ( **\_\_stdcall** C++ メソッドの呼び出し)

    関数のパラメーターは、左、右プッシュ、スタックで渡され、"this"ポインターがスタックにプッシュし、関数が呼び出されています。 呼び出し先がスタックを消去します。

-   **\_\_fastcall**

    最初の 2 つの DWORD またはより小さい引数が渡された、 **ecx**と**edx**を登録します。 残りのパラメーターは、左に右プッシュ、スタックに渡されます。 呼び出し先がスタックを消去します。

-   **\_\_cdecl**

    関数のパラメーターは、左、右プッシュ、スタックに渡され、呼び出し元がスタックを消去します。 **\_\_Cdecl**可変長のパラメーターを持つすべての関数の使用は、呼び出し規約。

### <a name="span-iddebuggerdisplayofregistersandflagsspanspan-iddebuggerdisplayofregistersandflagsspanspan-iddebuggerdisplayofregistersandflagsspandebugger-display-of-registers-and-flags"></a><span id="Debugger_Display_of_Registers_and_Flags"></span><span id="debugger_display_of_registers_and_flags"></span><span id="DEBUGGER_DISPLAY_OF_REGISTERS_AND_FLAGS"></span>デバッガーのレジスタとフラグの表示

サンプル デバッガーの登録の表示を次に示します。

```dbgcmd
eax=00000000 ebx=008b6f00 ecx=01010101 edx=ffffffff esi=00000000 edi=00465000
eip=77f9d022 esp=05cffc48 ebp=05cffc54 iopl=0         nv up ei ng nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000286
```

ユーザー モードのデバッグでは無視できます、**に対しては iopl**とデバッガーの表示の全体の最後の行。

### <a name="span-idx86-flagsspanspan-idx86flagsspanx86-flags"></a><span id="x86-flags"></span><span id="X86_FLAGS"></span>x86 フラグします。

2 番目の行の最後に 2 文字コードは、前の例では、*フラグ*します。 これらは単一ビット レジスタであり、さまざまな使用を持っています。

次のテーブルのリスト、x86 フラグ:

コードのフラグ名値フラグ状態の状態の説明をフラグ**の**

オーバーフロー フラグ

0 1 **nvov**

オーバーフローなしオーバーフロー **df**

方向フラグ

0 1 **updn**

下方向の方向**場合**

割り込みフラグ

0 1 **diei**

割り込みを有効にする割り込みを無効になっている**sf**

記号フラグ

0 1 **plng**

正の値 (または 0) 負**な zf**

0 個のフラグ

0 1 **nzzr**

0 以外の場合 0 **af**

補助キャリー フラグ

0 1 **naac**

補助を持たない補助キャリー **pf**

パリティ フラグ

0 1 **pepo**

パリティ偶数のパリティ奇数**cf**

フラグを実行します。

0 1 **nccy**

いない繰キャリー **tf**

トラップ フラグ

場合**tf** 1 と等しい、プロセッサが状態を発生させる\_単一\_1 つの命令の実行後にステップの例外。 このフラグは、シングル ステップのトレースを実装するために、デバッガーによって使用されます。 他のアプリケーションで使用する必要がありますされません。

**に対しては iopl**

I/O の特権レベル

これは、0 ~ 3 の範囲の値を持つ、two-bit の整数です。 ハードウェアへのアクセスを制御する、オペレーティング システムによって使用されます。 アプリケーションで使用する必要がありますされません。

 

レジスタは、デバッガー コマンド ウィンドウでいくつかのコマンドの結果として表示される、ときに、*フラグの状態*が表示されます。 ただし、フラグを使用して変更する場合、 [ **r (レジスタ)** ](r--registers-.md)コマンドを使用することによってを参照してください、*コード フラグを設定*します。

WinDbg の [レジスタ] ウィンドウでは、フラグ コードを使用して、表示またはフラグを変更します。 フラグの状態がサポートされていません。

次に例を示します。 上記の「登録フラグ状態の表示、 **ng**が表示されます。 これは、記号のフラグが 1 に設定されて現在いることを意味します。 これを変更するには、次のコマンドを使用します。

```dbgcmd
r sf=0
```

記号のフラグを 0 に設定します。 別のレジスタ表示を行う場合、 **ng**状態コードは表示されません。 代わりに、 **pl**状態コードが表示されます。

記号フラグ、0 フラグ、および伝達フラグは一般的に使用されるフラグです。

### <a name="span-idconditionsspanspan-idconditionsspanspan-idconditionsspanconditions"></a><span id="Conditions"></span><span id="conditions"></span><span id="CONDITIONS"></span>条件

A*条件*の 1 つまたは複数のフラグの状態について説明します。 X86 上のすべての条件付き操作の条件で表現されます。

アセンブラーでは、1 つまたは 2 つの文字の略語を使用して、条件を表します。 条件は、複数の省略形で表現できます。 たとえば、AE ("上記 or equal") は、NB (「いない下記」) と同じ条件です。 次の表は、いくつかの一般的な条件とその意味を示します。

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
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Z</p></td>
<td align="left"><p>な ZF = 1</p></td>
<td align="left"><p>最後の操作の結果には 0 でした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NZ</p></td>
<td align="left"><p>な ZF = 0</p></td>
<td align="left"><p>最後の操作の結果はゼロではありませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p>最後の操作は実行に必要なまたは借用します。 (符号なし整数の場合、これを示すオーバーフロー。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>NC</p></td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p>最後の操作の実行が必要または借用していません。 (符号なし整数の場合、これを示すオーバーフロー。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>SF = 1</p></td>
<td align="left"><p>最後の操作の結果は、設定、高ビットを持ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS</p></td>
<td align="left"><p>SF = 0</p></td>
<td align="left"><p>最後の操作の結果は、クリア、高ビットを持ちます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>O</p></td>
<td align="left"><p>1 を =</p></td>
<td align="left"><p>符号付き整数の操作として扱われます場合、最後の操作には、オーバーフローまたはアンダー フローが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用不可</p></td>
<td align="left"><p>0 を =</p></td>
<td align="left"><p>符号付き整数の操作として扱われます、ときに、最後の操作が発生しなかったオーバーフローまたはアンダー フロー。</p></td>
</tr>
</tbody>
</table>

 

条件が 2 つの値を比較することもできます。 **Cmp**命令が 2 つのオペランドを比較し、他の 1 つのオペランドを減算する場合と同様にフラグを設定します。 次の条件は、の結果を確認するために使用できます**cmp** *value1*、 *value2*します。

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
<th align="left">CMP 操作後に意味します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>な ZF = 1</p></td>
<td align="left"><p><em>value1</em> == <em>value2</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NE</p></td>
<td align="left"><p>な ZF = 0</p></td>
<td align="left"><p><em>value1</em> != <em>value2</em>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
GE NL</td>
<td align="left"><p>SF の =</p></td>
<td align="left"><p></p>
<em>value1</em> &gt; =  <em>value2</em>します。
値は、符号付き整数として扱われます。</td>
</tr>
<tr class="even">
<td align="left"><p></p>
LE NG</td>
<td align="left"><p>な ZF = 1 または SF! = の</p></td>
<td align="left"><p><em>value1</em> &lt; =  <em>value2</em>します。 値は、符号付き整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
G NLE</td>
<td align="left"><p>な ZF = 0 と SF を =</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>します。 値は、符号付き整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
L NGE</td>
<td align="left"><p>SF! =</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>します。 値は、符号付き整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
AE NB</td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p><em>value1</em> &gt; =  <em>value2</em>します。 値は、符号なし整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
NA をします。</td>
<td align="left"><p>CF = 1 またはな ZF = 1</p></td>
<td align="left"><p><em>value1</em> &lt; =  <em>value2</em>します。 値は、符号なし整数として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
と、</td>
<td align="left"><p>CF = 0 およびな ZF = 0</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>します。 値は、符号なし整数として扱われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
B NAE</td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>します。 値は、符号なし整数として扱われます。</p></td>
</tr>
</tbody>
</table>

 

条件は、通常の結果を操作に使用する**cmp**または**テスト**命令。 以下に例を示します。

```asm
cmp eax, 5
jz equal
```

比較、 **eax** 、式を計算して数 5 に対して登録 (**eax** - 5) 結果に従ったフラグの設定。 減算の結果が 0 の場合、 **zr**フラグが設定されます、 **jz**ジャンプが実行されるため、条件が true になります。

### <a name="span-iddatatypesspanspan-iddatatypesspanspan-iddatatypesspandata-types"></a><span id="Data_Types"></span><span id="data_types"></span><span id="DATA_TYPES"></span>データ型

-   バイト。8 ビット

-   word:16 ビット

-   dword:32 ビット

-   qword:64 ビット (2 倍の浮動小数点を含む)

-   tword:80 ビット (拡張の倍精度浮動小数点数を含む)

-   oword:128 ビット

### <a name="span-idnotationspanspan-idnotationspanspan-idnotationspannotation"></a><span id="Notation"></span><span id="notation"></span><span id="NOTATION"></span>表記法

次の表では、アセンブリ言語命令を記述するために使用する表記法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表記法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>r</strong>、 <strong>r1</strong>、 <strong>r2</strong>.</p></td>
<td align="left"><p>レジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>メモリ アドレス (詳細については、後続のアドレッシング モード」を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#n</p></td>
<td align="left"><p>イミディ エイト定数</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>登録またはメモリ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r</strong>/#n</p></td>
<td align="left"><p>登録または即時定数</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>レジスタ、メモリ、または即時定数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>cc</em></p></td>
<td align="left"><p>上記の条件のセクションに記載する条件コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>T</em></p></td>
<td align="left"><p>"B"、"W"または"D"(バイト、ワード、dword)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>acc<em>T</em></p></td>
<td align="left"><p>サイズ<em>T</em>アキュムレータ: <strong>al</strong>場合<em>T</em> ="B"、 <strong>ax</strong>場合<em>T</em> ="W"または<strong>eax</strong>場合<em>T</em> "D"を =</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaddressingmodesspanspan-idaddressingmodesspanspan-idaddressingmodesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>アドレッシング モード

いくつかの別のアドレッシング モードがありますが、フォームを受け取る**T ptr \[expr\]** ここで、 **T**一部のデータ (データ型の前のセクションを参照してください) を入力および**expr**定数およびレジスタに関連するいくつかの式です。

それほど難しくないほとんどのモードの表記法を推測できます。 たとえば、**バイト PTR \[esi + edx\*8 + 3\]** 意味"の値を取得、 **esi**登録、8 回の値を追加して、 **edx**を登録し、3 つの追加、結果として得られるアドレスにあるバイトにアクセスします"。

### <a name="span-idpipeliningspanspan-idpipeliningspanspan-idpipeliningspanpipelining"></a><span id="Pipelining"></span><span id="pipelining"></span><span id="PIPELINING"></span>パイプライン処理

Pentium は、1 つのクロックのティックで最大 2 つのアクションを実行できることを意味するデュアル問題です。 ただし、一度に 2 つのアクションの処理を実行できる場合の規則 (と呼ばれる*ペアリング*) が非常に複雑です。

X86 が CISC プロセッサであるために、ジャンプ遅延スロットについて心配する必要はありません。

### <a name="span-idsynchronizedmemoryaccessspanspan-idsynchronizedmemoryaccessspanspan-idsynchronizedmemoryaccessspansynchronized-memory-access"></a><span id="Synchronized_Memory_Access"></span><span id="synchronized_memory_access"></span><span id="SYNCHRONIZED_MEMORY_ACCESS"></span>同期されたメモリへのアクセス

読み込み、変更、および格納指示が受け取れる、**ロック**プレフィックスで、次のように命令を変更します。

1.  命令を発行する前に、CPU は一貫性を確保するすべての保留中のメモリ操作をフラッシュします。 すべてのデータのプリフェッチが破棄されました。

2.  命令を発行する際に、CPU はバスへの排他アクセスがあります。 これにより、読み込み/変更/ストア操作の原子性です。

**Xchg**メモリを持つ値が交換されるたびに、前の規則が命令によって自動的に従います。

既定でその他のすべての命令 nonlocking します。

### <a name="span-idjumppredictionspanspan-idjumppredictionspanspan-idjumppredictionspanjump-prediction"></a><span id="Jump_Prediction"></span><span id="jump_prediction"></span><span id="JUMP_PREDICTION"></span>予測をジャンプします。

無条件ジャンプを予測して、実行します。

未受講または実行すると予測されます。 条件付きのジャンプ、実行された最終時刻を作成したかどうかによって異なります。 ジャンプの履歴を記録するため、キャッシュ サイズが制限されています。

CPU が条件付きのジャンプを取得またはが実行された最終時刻になっていないかどうかの記録を持たない場合、旧バージョンと条件付きのジャンプを予測として扱わし、実行しない条件付きのジャンプを転送します。

### <a name="span-idalignmentspanspan-idalignmentspanspan-idalignmentspanalignment"></a><span id="Alignment"></span><span id="alignment"></span><span id="ALIGNMENT"></span>配置

X86 プロセッサでは、パフォーマンスの低下にアラインされていないメモリへのアクセスを自動的に修正されます。 例外は発生しません。

メモリ アクセスは、アドレスが整数である場合の配置と見なされます、オブジェクトのサイズの倍数です。 たとえば、バイトのすべてのアクセスを配置 (整数すべてが 1 の倍数)、アドレスを均等に WORD へのアクセスが揃えられ、DWORD アドレス配置するには 4 の倍数である必要があります。

**ロック**アラインされていないメモリ アクセスのプレフィックスを使用しない必要があります。

 

 





