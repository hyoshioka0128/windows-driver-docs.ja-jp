---
title: dt (表示の種類)
description: Dt コマンドには、ローカル変数、グローバル変数またはデータ型に関する情報が表示されます。 これにより、単純なデータの型だけでなく構造体と共用体についての情報が表示できます。
ms.assetid: 82aba13e-6604-46ca-b3e5-bb865ecf3f1f
keywords:
- dt (表示の種類) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dt (Display Type)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5ee88b52ddfe5a3d843d7c82d89cf69afc795bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548952"
---
# <a name="dt-display-type"></a>dt (表示の種類)


**Dt**コマンドは、ローカル変数、グローバル変数またはデータ型に関する情報を表示します。 これにより、単純なデータの型だけでなく構造体と共用体についての情報が表示できます。

ユーザー モードの構文

```dbgcmd
dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

カーネル モードの構文

```dbgcmd
[Processor] dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

## <a name="span-idddkcmddisplaytypedbgspanspan-idddkcmddisplaytypedbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
必要な情報を格納しているプロセスを実行しているプロセッサを指定します。 詳細については、[マルチプロセッサ構文](multiprocessor-syntax.md)を参照してください。 プロセッサは、カーネル モードでのみ指定できます。

<span id="_______DisplayOpts______"></span><span id="_______displayopts______"></span><span id="_______DISPLAYOPTS______"></span> *DisplayOpts*   
次の表で指定したオプションの 1 つ以上を指定します。 これらのオプションには、ハイフンが付きます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-a</strong>[<em>quantity</em>]</p></td>
<td align="left"><p>インデックスで、新しい行で配列の各要素を表示します。 合計<em>数量</em>要素が表示されます。 間にスペースが必要ない、 <strong>、</strong>と<em>数量</em>します。 場合<strong>-a</strong>に従わない、数字が配列内のすべての項目が表示されます。 <strong>-A</strong>[<em>数量</em>] スイッチがこの方法で表示する前に、それぞれの型名またはフィールド名をすぐに表示する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>ブロックを再帰的に表示します。 表示されている構造体にサブ構造体が含まれている場合は任意の深さを再帰的に展開し、完全に表示されます。 サブ構造体ではなく、元の構造内にある場合にのみ、ポインターが展開されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>出力を最適化します。 すべてのフィールドは、可能であれば、1 行に表示されます。 (を使用すると、 <strong>-a</strong>スイッチ、配列の各要素は、複数行ブロックとして書式設定されるのではなく、1 つの行)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>使用すると、<em>名前</em>にアスタリスクが付いているが終了したで始まるすべての種類の詳細な出力を表示、<em>名前</em>。 場合<em>名前</em>しないアスタリスクで終わる、詳細な出力を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>強制<strong>dt</strong>型を列挙します。 場合にのみ、このオプションが必要<strong>dt</strong>が誤って解釈している、<em>名前</em>型ではなくインスタンスとして値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-i</strong></p></td>
<td align="left"><p>サブタイプをインデントしません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-o</strong></p></td>
<td align="left"><p>構造体のフィールドのオフセット値を省略します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-p</strong></p></td>
<td align="left"><p><em>アドレス</em>仮想アドレスではなく、物理アドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-r</strong>[<em>depth</em>]</p></td>
<td align="left"><p>再帰的には、サブタイプのフィールドをダンプします。 場合<em>深さ</em>は、この再帰が停止後<em>深さ</em>レベル。 <em>深さ</em>1 から 9 までの数字にする必要がありの間には空白が存在する必要があります、 <strong>r</strong>と<em>深さ</em>します。 <strong>-R</strong>[<em>深さ</em>] スイッチは、アドレスの前にすぐに表示する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong> <em>サイズ</em></p></td>
<td align="left"><p>Equals のバイトの値でそのサイズにタイプもののみを列挙<em>サイズ</em>します。 <strong>-S</strong>オプションは、型が列挙されている場合にのみ便利です。 ときに<strong>-s</strong>が指定されている<strong>-e</strong>は常に暗黙にもします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>型のみを列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>詳細な出力。 これにより、構造体と、その要素の数の合計サイズなどの追加情報です。 と共に使用されるこの、 <strong>-y</strong>検索オプションをすべてのシンボルが表示されますも関連付けられている型の情報がありません。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______SearchOpts______"></span><span id="_______searchopts______"></span><span id="_______SEARCHOPTS______"></span> *SearchOpts*   
次の表で指定したオプションの 1 つ以上を指定します。 これらのオプションには、ハイフンが付きます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-n</strong></p></td>
<td align="left"><p>これは、次のパラメーターが名であることを示します。 これは、使用してくださいの 16 進数の文字だけの次の項目が構成されている場合がそれ以外の場合、アドレスとして実行するためです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-y</strong></p></td>
<td align="left"><p>これは、次のパラメーターが名、名前は必ずしも全体の先頭であることを示します。 ときに<strong>-y</strong>に含まれているすべての一致項目が一覧表示されます、リスト内の最初の一致で詳細情報の後にします。 場合<strong>-y</strong>が含まれていない場合、完全一致のみが表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
この構造体を定義するモジュールを指定する、省略可能なパラメーター。 含める必要がある場合は、ローカル変数またはグローバル変数または型と同じ名前の型がある、*モジュール*グローバル変数を意味することを指定します。 それ以外の場合、 **dt**コマンド場合でも、ローカル変数が、大文字と小文字およびグローバル変数は大文字小文字を区別、ローカル変数が表示されます。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
種類またはグローバル変数の名前を指定します。 場合*名前*末尾がアスタリスク (**\\* * *)、すべての一致項目の一覧が表示されます。したがって、 **dt A\\***  すべてのデータ型、グローバル変数、および"A"で静的変数の先頭に一覧表示されますが、これらの型の実際のインスタンスは表示されません。 (場合、 **-v**表示オプションが同時に使用される、すべてのシンボルが表示されます - 型情報が関連付けられている人だけでなく)。置換することもできます*名前*にピリオド (**.**) 最近繰り返すことを示すための値を使用*名前*。

場合*名前*、空白文字を含めることは、かっこで囲む必要があります。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span> *フィールド*   
表示するフィールドを指定します。 場合*フィールド*は省略すると、すべてのフィールドが表示されます。 場合*フィールド*ピリオドが続く (**.**)、このフィールドの最初のレベルのサブフィールドにも表示されます。 場合*フィールド*の後に深さまでの期間の数に等しい一連の期間のサブフィールドが表示されます。 ピリオドが続くすべてのフィールド名は、プレフィックス一致として扱われます場合と、 **-y**検索オプションを使用しました。 場合*フィールド*アスタリスクが続きます (\*)、フィールド、必ずしも全体のフィールドの先頭のみとして扱われ、一致するすべてのフィールドが表示されます。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示される構造体のアドレスを指定します。 場合*名前*を省略すると、*アドレス*含める必要があるし、グローバル変数のアドレスを指定する必要があります。 *アドレス*は指定しない限り仮想アドレスを取得します。 使用して、 **-p**物理アドレスを指定するオプション。 "At"記号を使用して ( **@** ) レジスタを指定する (たとえば、 <strong>@eax</strong>)。

<span id="_______List______"></span><span id="_______list______"></span><span id="_______LIST______"></span> *一覧*   
リンクされたリストをリンクしているフィールド名を指定します。 *アドレス*パラメーターを含める必要があります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>注釈
-------

**Dt**コマンドの出力が基本 10、および 16 進数の符号なし数値の符号付き数値を常に表示されます。

すべてのパラメーター **dt**シンボル値には文字列のワイルドカードが許可することもできます。 参照してください[文字列のワイルドカード構文](string-wildcard-syntax.md)詳細についてはします。

**-Y**と **-n**オプションはいずれかを前に指定できる*名前*または*フィールド*します。 **-Y**オプションでは、型または構造体の名前の先頭を指定できます。 たとえば、 **dt y ALLEN**の種類に関するデータが表示されます**アレンタウン**します。 、、型がない表示する可能性があります**アレンタウン**で**dt y A**します。使用する必要が代わりに、 **dt -ny A**ため、 **A**有効な 16 進数の値は、なし、アドレスとして解釈される、 **-n**オプション。

場合*名前*構造体を示しますのすべてのフィールドが表示されます (たとえば、 **dt myStruct**)。 特定の 1 つのフィールドが欲しい場合**dt myStruct myField**します。 C を呼び出すメンバーが表示されます**myStruct.myField**します。 ただし、コマンドは、 **dt myStruct myField1 myField2**表示**myStruct.myField1**と**myStruct.myField2**。 表示されない**myStruct.myField1.myField2**します。

構造体名またはフィールドは、添字に続けて、これと配列の 1 つのインスタンスを指定します。 たとえば、 **dt myStruct myFieldArray\[3\]** 問題の配列の 4 番目の要素が表示されます。 型名には、添字が続く、これと配列全体を指定します。 たとえば、 **dt CHAR\[8\] myPtr** 8 文字の文字列が表示されます。 常に、添字が取得されます現在の基数に関係なく 10 進数として。**0 x**プレフィックスには、エラーが発生します。

コマンドからの型情報を使用しているため、します。*pdb*ファイル、任意の CPU プラットフォームのデバッグを自由に使用できます。

使用される型情報**dt**で作成されたすべての型名に含まれる**typedef**、すべての Windows 定義型を含むです。 たとえば、 **unsigned long**と**char** 、有効な型名ではありませんが**ULONG**と**CHAR**は。 名前を入力するすべての Windows の完全な一覧については Microsoft Windows SDK を参照してください。

によって作成されたすべての種類**typedef**独自コード内に表示されます、プログラムで実際に使用されている限り、します。 ただし、ヘッダーで定義されているが、実際に使用される型は、.pdb シンボル ファイルでは保存されません、デバッガーにアクセスできなくなります。 このような型をデバッガーに使用できるようにするとしてを使用して、*入力*の**typedef**ステートメント。 たとえば、次のコード、MY 構造体で、次が表示されます\_データ .pdb シンボル ファイルに格納され、表示されることができます、 **dt**コマンド。

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA;
typedef  MY_DATA *PMY_DATA; 
```

その一方で、次のコードは不十分なため、両方の MY\_データと PMY\_によって初期データが定義されている**typedef**と、そのため、MY\_データ自体使用されていないの入力としてすべて**typedef**ステートメント。

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA, *PMY_DATA; 
```

いずれの場合も、型情報は、すべてのプライベート シンボル情報が削除されているシンボル ファイルではなく、完全なシンボル ファイルにのみ含まれます。 詳細については、[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)を参照してください。

Unicode 文字列を表示する場合は、使用する必要があります、 [**リストア\_(Unicode 表示を有効にする) unicode** ](-enable-unicode--enable-unicode-display-.md)最初コマンドします。 長整数の表示を制御することができます、 [**リストア\_長い\_ステータス (有効にする Long 整数を表示する)** ](-enable-long-status--enable-long-integer-display-.md)コマンド。

次の例では、 **dt**グローバル変数が表示されます。

```dbgcmd
0:000> dt mt1 
   +0x000 a                : 10
   +0x004 b                : 98 'b'
   +0x006 c                : 0xdd
   +0x008 d                : 0xabcd
   +0x00c gn               : [6] 0x1
   +0x024 ex               : 0x0 
```

次の例では、 **dt**配列フィールドが表示されます**gn**:

```dbgcmd
0:000> dt mt1 -a gn 
   +0x00c gn : 
    [00] 0x1
    [01] 0x2
    [02] 0x3
    [03] 0x4
    [04] 0x5
    [05] 0x6 
```

次のコマンドは、変数のいくつかのサブフィールドを表示します。

```dbgcmd
0:000> dt mcl1 m_t1 dpo 
   +0x010 dpo  : DEEP_ONE
   +0x070 m_t1 : MYTYPE1 
```

次のコマンド表示フィールドのサブフィールド**m\_t1**します。 始まる任意のフィールドのサブフィールドも表示されます、期間は、プレフィックス一致により自動的に発生するため"m\_t1"。

```dbgcmd
0:000> dt mcl1 m_t1. 
   +0x070 m_t1  : 
      +0x000 a     : 0
      +0x004 b     : 0 '
      +0x006 c     : 0x0
      +0x008 d     : 0x0
      +0x00c gn    : [6] 0x0
      +0x024 ex    : 0x0 
```

これは、任意の深さまで繰り返しますでした。 たとえば、次のコマンド**dt mcl1、..c。** 最初のフィールド名が開始されるように 4 つの深さまですべてのフィールドを表示は **、** で開始しますが、3 番目のフィールド名と**c**します。

サブフィールドの表示方法の詳細な例を次に示します。 最初に、表示、 **Ldr**フィールド。

```dbgcmd
0:000> dt nt!_PEB Ldr 7ffdf000 
   +0x00c Ldr : 0x00191ea0 
```

これで、ポインター型のフィールドを展開します。

```dbgcmd
0:000> dt nt!_PEB Ldr Ldr. 7ffdf000 
   +0x00c Ldr  : 0x00191ea0
      +0x000 Length : 0x28
      +0x004 Initialized : 0x1 '
      +0x008 SsHandle : (null)
      +0x00c InLoadOrderModuleList : _LIST_ENTRY [ 0x191ee0 - 0x192848 ]
      +0x014 InMemoryOrderModuleList : _LIST_ENTRY [ 0x191ee8 - 0x192850 ]
      +0x01c InInitializationOrderModuleList : _LIST_ENTRY [ 0x191f58 - 0x192858 ]
      +0x024 EntryInProgress : (null) 
```

表示されるように、 **CriticalSectionTimeout**フィールド。

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout 7ffdf000 
   +0x070 CriticalSectionTimeout : _LARGE_INTEGER 0xffffe86d`079b8000 
```

今すぐ展開、 **CriticalSectionTimeout**サブフィールド 1 レベル深い構造体します。

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout. 7ffdf000 
   +0x070 CriticalSectionTimeout  :  0xffffe86d`079b8000
      +0x000 LowPart                 : 0x79b8000
      +0x004 HighPart                : -6035
      +0x000 u                       : __unnamed
      +0x000 QuadPart                : -25920000000000 
```

今すぐ展開、 **CriticalSectionTimeout**サブフィールド 2 つのレベルが深い構造体します。

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout.. 7ffdf000 
   +0x070 CriticalSectionTimeout   :  0xffffe86d`079b8000
      +0x000 LowPart                  : 0x79b8000
      +0x004 HighPart                 : -6035
      +0x000 u                        :
         +0x000 LowPart                  : 0x79b8000
         +0x004 HighPart                 : -6035
      +0x000 QuadPart                 : -25920000000000 
```

次のコマンドでは、MYTYPE1 0x0100297C アドレスにあるデータ型のインスタンスが表示されます。

```dbgcmd
0:000> dt 0x0100297c MYTYPE1 
   +0x000 a                : 22
   +0x004 b                : 43 '+'
   +0x006 c                : 0x0
   +0x008 d                : 0x0
   +0x00c gn               : [6] 0x0
   +0x024 ex               : 0x0 
```

次のコマンドでは、アドレス 0x01002BE0 で 10 ULONGs の配列を表示します。

```dbgcmd
0:000> dt -ca10 ULONG 01002be0 
[0] 0x1001098
[1] 0x1
[2] 0xdead
[3] 0x7d0
[4] 0x1
[5] 0xcd
[6] 0x0
[7] 0x0
[8] 0x0
[9] 0x0 
```

次のコマンドでは、別のアドレスで以前の表示が続行されます。 "ULONG"が再入力する必要がないことに注意してください。

```dbgcmd
0:000> dt -ca4 . 01002d00 
Using sym ULONG
[0] 0x12
[1] 0x4ac
[2] 0xbadfeed
[3] 0x2 
```

型の表示の例をいくつかを示します。 次のコマンド モジュールのすべての型と文字列"MY"以降のグローバル変数を表示する*モジュール*します。 実際のインスタンスをアドレス プレフィックスアドレスがないものは、型定義を示します。

```dbgcmd
0:000> dt thismodule!MY* 
010029b8  thismodule!myglobal1
01002990  thismodule!myglobal2
          thismodule!MYCLASS1
          thismodule!MYCLASS2
          thismodule!MYCLASS3
          thismodule!MYTYPE3::u
          thismodule!MYTYPE1
          thismodule!MYTYPE3
          thismodule!MYTYPE3
          thismodule!MYFLAGS 
```

型の表示を実行するときに、 **-v**各項目のサイズを表示するオプションを使用できます。 **-S** *サイズ*のみ、特定のサイズの項目を列挙するオプションを使用できます。 ここでも、アドレス プレフィックスは実際のインスタンスアドレスがないものは、型定義を示します。

```dbgcmd
0:001> dt -s 2 -v thismodule!* 
Enumerating symbols matching thismodule!*, Size = 0x2
Address   Size Symbol
           002 thismodule!wchar_t
           002 thismodule!WORD
           002 thismodule!USHORT
           002 thismodule!SHORT
           002 thismodule!u_short
           002 thismodule!WCHAR
00427a34   002 thismodule!numberOfShips
00427a32   002 thismodule!numberOfPlanes
00427a30   002 thismodule!totalNumberOfItems 
```

次の例に示します、 **-b**オプション。 構造が展開、 **OwnerThreads**構造内の配列を展開するが、 **Flink**と**点滅**リスト ポインターが後にありません。

```dbgcmd
kd> dt nt!_ERESOURCE -b 0x8154f040 
   +0x000 SystemResourcesList :  [ 0x815bb388 - 0x816cd478 ]
      +0x000 Flink            : 0x815bb388
      +0x004 Blink            : 0x816cd478
   +0x008 OwnerTable       : (null)
   +0x00c ActiveCount      : 1
   +0x00e Flag             : 8
   +0x010 SharedWaiters    : (null)
   +0x014 ExclusiveWaiters : (null)
   +0x018 OwnerThreads     :
    [00]
      +0x000 OwnerThread      : 0
      +0x004 OwnerCount       : 0
      +0x004 TableSize        : 0
    [01]
      +0x000 OwnerThread      : 0x8167f563
      +0x004 OwnerCount       : 1
      +0x004 TableSize        : 1
   +0x028 ContentionCount  : 0
   +0x02c NumberOfSharedWaiters : 0
   +0x02e NumberOfExclusiveWaiters : 0
   +0x030 Address          : (null)
   +0x030 CreatorBackTraceIndex : 0
   +0x034 SpinLock         : 0
```

次の例に示します**dt**カーネル モードでします。 次のコマンドと同様の結果を生成する[ **! process 0 0**](-process.md):

```dbgcmd
kd> dt nt!_EPROCESS -l ActiveProcessLinks.Flink -y Ima -yoi Uni 814856f0 
## ActiveProcessLinks.Flink at 0x814856f0

UniqueProcessId : 0x00000008
ImageFileName : [16] "System"

## ActiveProcessLinks.Flink at 0x8138a030

UniqueProcessId : 0x00000084
ImageFileName : [16] "smss.exe"

## ActiveProcessLinks.Flink at 0x81372368

UniqueProcessId : 0x000000a0
ImageFileName : [16] "csrss.exe"

## ActiveProcessLinks.Flink at 0x81369930

UniqueProcessId : 0x000000b4
ImageFileName : [16] "winlogon.exe"

.... 
```

一覧の各要素に対してコマンドを実行する場合を使用して、 [ **! 一覧**](-list.md)拡張機能。

最後に、 **dt-h**コマンドの短いヘルプ テキストの要約が表示されます、 **dt**構文。

 

 





