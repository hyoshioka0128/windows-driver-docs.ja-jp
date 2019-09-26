---
title: dt (型の表示)
description: Dt コマンドでは、ローカル変数、グローバル変数、またはデータ型に関する情報が表示されます。 これにより、単純なデータ型に加え、構造と共用体に関する情報を表示できます。
ms.assetid: 82aba13e-6604-46ca-b3e5-bb865ecf3f1f
keywords:
- dt (表示の種類) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dt (Display Type)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa4ac5a62cd92c108b1c33725dbdc35b0c883f75
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284968"
---
# <a name="dt-display-type"></a>dt (型の表示)


**Dt**コマンドでは、ローカル変数、グローバル変数、またはデータ型に関する情報が表示されます。 これにより、単純なデータ型に加え、構造と共用体に関する情報を表示できます。

ユーザーモードの構文

```dbgcmd
dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

カーネルモード構文

```dbgcmd
[Processor] dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

## <a name="span-idddk_cmd_display_type_dbgspanspan-idddk_cmd_display_type_dbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>パラメータ


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*プロセッサ*   
必要な情報が含まれているプロセスを実行しているプロセッサを指定します。 詳細については、「[マルチプロセッサ構文](multiprocessor-syntax.md)」を参照してください。 プロセッサはカーネルモードでのみ指定できます。

<span id="_______DisplayOpts______"></span><span id="_______displayopts______"></span><span id="_______DISPLAYOPTS______"></span>*Displaydisplay*   
次の表に示す1つ以上のオプションを指定します。 これらのオプションの前にはハイフンが付きます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OPTION</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-a</strong>[<em>quantity</em>]</p></td>
<td align="left"><p>各配列要素をインデックスと共に新しい行に表示します。 <em>数量</em>要素の合計が表示されます。 <strong>A</strong>と<em>quantity</em>の間にスペースを配置することはできません。 <strong>-A</strong>の後に数字が付いていない場合は、配列内のすべての項目が表示されます。 <strong>-A</strong>[<em>quantity</em>] スイッチは、この方法で表示する各型名またはフィールド名の直前に表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>ブロックを再帰的に表示します。 表示されている構造体にサブ構造体が含まれている場合は、任意の深度に再帰的に展開され、完全に表示されます。 ポインターは、サブ構造体ではなく元の構造にある場合にのみ拡張されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>圧縮出力。 可能であれば、すべてのフィールドが1行に表示されます。 ( <strong>-A</strong>スイッチと共に使用する場合、各配列要素は、複数行のブロックとして書式設定されるのではなく、1つの行を受け取ります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>アスタリスクで終わっている<em>名前</em>で使用する場合は、 <em>name</em>で始まるすべての型の詳細出力を表示します。 <em>名前</em>の末尾にアスタリスクが付いていない場合は、詳細出力を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p><strong>Dt</strong>が型を列挙するように強制します。 このオプションは、 <strong>dt</strong>によって<em>名前</em>の値が型ではなくインスタンスとして誤って解釈される場合にのみ必要です。</p></td>
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
<td align="left"><p><em>アドレス</em>は、仮想アドレスではなく、物理アドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-r</strong>[<em>詳細</em>]</p></td>
<td align="left"><p>サブタイプフィールドを再帰的にダンプします。 <em>Depth</em>が指定されている場合、この再帰は<em>深さ</em>レベルの後に停止します。 <em>深さ</em>は1から9までの数字にする必要があります。また、 <strong>r</strong>と<em>depth</em>の間にスペースを配置することはできません。 <strong>-R</strong>[<em>depth</em>] スイッチは、アドレスの直前に表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong><em>サイズ</em></p></td>
<td align="left"><p>バイト単位のサイズが<em>size</em>の値と等しい型のみを列挙します。 <strong>-S</strong>オプションは、型が列挙されている場合にのみ有効です。 <strong>-S</strong>が指定されている場合、 <strong>-e</strong>も常に暗黙的に指定されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>型のみを列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>詳細出力。 これにより、構造体の合計サイズや要素の数などの追加情報が提供されます。 これを<strong>-y</strong>検索オプションと共に使用すると、型情報が関連付けられていないものも含め、すべての記号が表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______SearchOpts______"></span><span id="_______searchopts______"></span><span id="_______SEARCHOPTS______"></span>*Searchopts*   
次の表に示す1つ以上のオプションを指定します。 これらのオプションの前にはハイフンが付きます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OPTION</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-n</strong></p></td>
<td align="left"><p>これは、次のパラメーターが名前であることを示します。 これは、次の項目がすべて16進文字で構成されている場合に使用します。それ以外の場合は、アドレスとして取得されるためです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-y</strong></p></td>
<td align="left"><p>これは、次のパラメーターが名前の先頭であり、必ずしも名前全体ではないことを示しています。 <strong>-Y</strong>が含まれている場合は、すべての一致が一覧表示され、その後、リスト内の最初の一致に関する詳細情報が示されます。 <strong>-Y</strong>が含まれていない場合は、完全一致のみが表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______module______"></span><span id="_______MODULE______"></span>*モジュール*   
この構造体を定義するモジュールを指定する省略可能なパラメーター。 グローバル変数または型と同じ名前のローカル変数または型がある場合は、グローバル変数を指定する*モジュール*を含める必要があります。 そうしないと、ローカル変数が大文字と小文字を区別せず、グローバル変数が大文字と小文字を区別する場合でも、 **dt**コマンドによってローカル変数が表示されます。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名前*   
型またはグローバル変数の名前を指定します。 *名前*の末尾にアスタリスク (\*) が付いている場合は、すべての一致の一覧が表示されます。 したがって、 **dt\\A*** は、"A" で始まるすべてのデータ型、グローバル、およびスタティックを一覧表示しますが、これらの型の実際のインスタンスは表示されません。 ( **-V** display オプションを同時に使用すると、関連付けられている型情報を持つシンボルだけでなく、すべての記号が表示されます)。また、 *name*をピリオド ( **.** ) に置き換えて、最近使用した*名前*の値を繰り返すように指定することもできます。

*名前*にスペースが含まれている場合は、かっこで囲む必要があります。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span>*フィールド*   
表示するフィールドを指定します。 *フィールド*を省略した場合は、すべてのフィールドが表示されます。 *フィールド*の後にピリオド ( **.** ) がある場合は、このフィールドの第1レベルサブフィールドも表示されます。 *フィールド*の後に一連のピリオドが続く場合、サブフィールドは期間の数と同じ深さに表示されます。 **-Y**検索オプションを使用した場合と同じように、フィールド名の後にピリオドが続くと、プレフィックスの一致として扱われます。 *フィールド*の後にアスタリスク (\*) がある場合は、フィールド全体ではなくフィールドの先頭のみとして扱われ、すべての一致するフィールドが表示されます。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示する構造体のアドレスを指定します。 *Name*を省略する場合は、 *address*を含め、グローバル変数のアドレスを指定する必要があります。 特に指定がない限り、*アドレス*は仮想アドレスとして使用されます。 物理アドレスを指定するには、 **-p**オプションを使用します。 レジスタを指定するには、 **@** アットマーク () を使用します ( <strong>@eax</strong>たとえば、)。

<span id="_______List______"></span><span id="_______list______"></span><span id="_______LIST______"></span>*リスト*   
リンクリストをリンクするフィールド名を指定します。 *Address*パラメーターを含める必要があります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリ操作の概要とその他のメモリ関連コマンドの説明については、「[メモリの読み取りと書き込み](reading-and-writing-memory.md)」を参照してください。

<a name="remarks"></a>コメント
-------

**Dt**コマンドの出力には、常に10進数の符号付き数値と16進数の符号なしの数値が表示されます。

シンボル値を許可する**dt**のすべてのパラメーターは、文字列のワイルドカードも許可します。 詳細については、「[文字列ワイルドカード構文](string-wildcard-syntax.md)」を参照してください。

**-Y**オプションと **-n**オプションは、任意の*名前*または*フィールド*の前に指定できます。 **-Y**オプションを使用すると、型または構造体の名前の先頭を指定できます。 たとえば、 **dt-y ALLEN**は、 **allentown**型に関するデータを表示します。 ただし、型**Allentown**を**Dt-y A**と共に表示することはできません。代わりに、 **dt-Ny a**を使用する必要があります。これは **、** が有効な16進数の値であり、 **-n**オプションを指定せずにアドレスとして解釈されるためです。

*名前*が構造体を示す場合は、すべてのフィールドが表示されます (たとえば、 **dt mystruct**)。 特定のフィールドが1つだけ必要な場合は、 **Dt myStruct myField**を実行できます。 これにより、C が**myField**を呼び出すメンバーが表示されます。 ただし、コマンド**Dt Mystruct MyField1 myField2**には**Mystruct. MyField1**と**mystruct. myField2**が表示されることに注意してください。 MyField1 は表示されません。 **myField2**。

構造体の名前またはフィールドの後に添字が続く場合は、配列の1つのインスタンスを指定します。 たとえば、 **dt mystruct\[myfieldarray 3\]** では、該当する配列の4番目の要素が表示されます。 しかし、型名の後に添字が続く場合は、配列全体を指定します。 たとえば、 **dt CHAR\[\] 8 myptr**は、8文字の文字列を表示します。 添字は、現在の基数に関係なく、常に小数点として取得されます。**0x**プレフィックスを付けると、エラーが発生します。

このコマンドは、からの型情報を使用するためです。*pdb*ファイルは、任意の CPU プラットフォームのデバッグに自由に使用できます。

**Dt**によって使用される型情報には、すべての Windows 定義型を含め、 **typedef**で作成されたすべての型名が含まれます。 たとえば、 **unsigned long**および**char**は有効な型名ではありませんが、 **ULONG**および**char**はです。 すべての Windows 型名の完全な一覧については、Microsoft Windows SDK を参照してください。

独自のコード内の**typedef**によって作成されたすべての型は、プログラムで実際に使用されている限り、存在します。 ただし、ヘッダーに定義されているものの、実際には使用されていない型は .pdb シンボルファイルに格納されず、デバッガーはアクセスできません。 このような型をデバッガーで使用できるようにするには、 **typedef**ステートメントの*入力*として使用します。 たとえば、コードに次のコードが含まれている場合、\_データの構造は .pdb シンボルファイルに格納され、 **dt**コマンドで表示できます。

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA;
typedef  MY_DATA *PMY_DATA; 
```

一方、次のコードで\_は、my data と pmy\_データの両方が初期の\_ **typedef**によって定義されているため、データ自体は**typedef**の入力として使用されていないため、十分ではありません。諸表

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA, *PMY_DATA; 
```

どのような場合でも、型情報は、すべてのプライベートシンボル情報が削除されたシンボルファイルではなく、完全なシンボルファイルにのみ含まれます。 詳細については、「[パブリックシンボルとプライベートシンボル](public-and-private-symbols.md)」を参照してください。

Unicode 文字列を表示する場合は、まず、 [ **. enable\_unicode (unicode 表示を有効**](-enable-unicode--enable-unicode-display-.md)にする) コマンドを使用する必要があります。 長い整数の表示を制御するには、を使用[**し\_ます。 long の状態\_を有効にする (長い整数の表示を有効にする)** ](-enable-long-status--enable-long-integer-display-.md)コマンドを有効にします。

次の例では、 **dt**はグローバル変数を表示します。

```dbgcmd
0:000> dt mt1 
   +0x000 a                : 10
   +0x004 b                : 98 'b'
   +0x006 c                : 0xdd
   +0x008 d                : 0xabcd
   +0x00c gn               : [6] 0x1
   +0x024 ex               : 0x0 
```

次の例では、 **dt**は配列フィールド**gn**を表示します。

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

次のコマンドは、変数のサブフィールドを表示します。

```dbgcmd
0:000> dt mcl1 m_t1 dpo 
   +0x010 dpo  : DEEP_ONE
   +0x070 m_t1 : MYTYPE1 
```

フィールド**m\_t1**のサブフィールドを表示するコマンドを次に示します。 ピリオドによってプレフィックスの一致が自動的に行われるため、"m\_t1" で始まる任意のフィールドのサブフィールドも表示されます。

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

これは、任意の深さに繰り返すことができます。 たとえば、コマンド**dt mcl1 a..c。** **では**、最初のフィールド名がで始まり、3番目のフィールド名が**c**で始まるように、すべてのフィールドが深さ4に表示されます。

ここでは、サブフィールドを表示する方法の詳細な例を示します。 最初に、 **Ldr**フィールドを表示します。

```dbgcmd
0:000> dt nt!_PEB Ldr 7ffdf000 
   +0x00c Ldr : 0x00191ea0 
```

次に、[ポインターの種類] フィールドを展開します。

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

次に、 **CriticalSectionTimeout**フィールドを表示します。

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout 7ffdf000 
   +0x070 CriticalSectionTimeout : _LARGE_INTEGER 0xffffe86d`079b8000 
```

次に、 **CriticalSectionTimeout**構造体のサブフィールドを1レベル詳細に展開します。

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout. 7ffdf000 
   +0x070 CriticalSectionTimeout  :  0xffffe86d`079b8000
      +0x000 LowPart                 : 0x79b8000
      +0x004 HighPart                : -6035
      +0x000 u                       : __unnamed
      +0x000 QuadPart                : -25920000000000 
```

ここで、 **CriticalSectionTimeout**構造体のサブフィールドを展開します。

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

次のコマンドを実行すると、アドレス0x0100297C にあるデータ型 MYTYPE1 のインスタンスが表示されます。

```dbgcmd
0:000> dt 0x0100297c MYTYPE1 
   +0x000 a                : 22
   +0x004 b                : 43 '+'
   +0x006 c                : 0x0
   +0x008 d                : 0x0
   +0x00c gn               : [6] 0x0
   +0x024 ex               : 0x0 
```

次のコマンドでは、アドレス0x01002BE0 の 10 ULONGs の配列が表示されます。

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

次のコマンドは、前の表示を別のアドレスで続行します。 "ULONG" を再入力する必要はないことに注意してください。

```dbgcmd
0:000> dt -ca4 . 01002d00 
Using sym ULONG
[0] 0x12
[1] 0x4ac
[2] 0xbadfeed
[3] 0x2 
```

次に、型 display の例をいくつか示します。 次のコマンドは、モジュール*thismodule*内の文字列 "MY" で始まるすべての型とグローバルを表示します。 アドレスがプレフィックスとして使用されるのは実際のインスタンスです。アドレスのないものは型定義です。

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

Type display を実行する場合は、 **-v**オプションを使用して各項目のサイズを表示できます。 **-S** *size*オプションは、特定のサイズの項目だけを列挙するために使用できます。 ここでも、アドレスがプレフィックスとして使用されるのは実際のインスタンスです。アドレスのないものは型定義です。

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

**-B**オプションの例を次に示します。 構造体が展開され、構造体内の**Ownerthreads**配列が拡張されていますが、 **Flink**と**点滅**の一覧のポインターは次のようになります。

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

カーネルモードの**dt**の例を次に示します。 次のコマンドを実行すると、 [ **! process 0 0**](-process.md)のような結果が生成されます。

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

リストの各要素に対してコマンドを実行する場合は、 [ **! list**](-list.md)拡張機能を使用します。

最後に、 **dt-h**コマンドを実行すると、 **dt**構文の概要を説明する短いヘルプテキストが表示されます。

 

 





