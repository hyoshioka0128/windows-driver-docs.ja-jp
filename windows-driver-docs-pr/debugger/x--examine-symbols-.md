---
title: x (シンボルの検証)
description: X コマンドでは、指定したパターンに一致するすべてのコンテキストで、シンボルが表示されます。
ms.assetid: 8c71c2ca-4a9d-43e4-91b3-f05b5475316d
keywords:
- x (シンボルの検証) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- x (Examine Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14cf8fe0e8af0ae4eefd8de0b99998e00c7d6284
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381922"
---
# <a name="x-examine-symbols"></a>x (シンボルの検証)


**X**コマンドは、指定したパターンに一致するすべてのコンテキストで、シンボルを表示します。

```dbgcmd
x [Options] Module!Symbol 
x [Options] *
```

## <a name="span-idddkcmdexaminesymbolsdbgspanspan-idddkcmdexaminesymbolsdbgspanparameters"></a><span id="ddk_cmd_examine_symbols_dbg"></span><span id="DDK_CMD_EXAMINE_SYMBOLS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
シンボルの検索オプションを指定します。 次のオプションの 1 つ以上を使用することができます。

<span id="_0"></span>**/0**  
各シンボルのアドレスのみが表示されます。

<span id="_1"></span>**/1**  
各シンボルの名前のみが表示されます。

<span id="_2"></span>**/2**  
アドレスと各シンボル (データ型ではありません) の名前のみが表示されます。

<span id="_D"></span><span id="_d"></span>**/D**  
使用して、出力が表示されます。[デバッガー Markup Language](debugger-markup-language-commands.md)します。

<span id="_t"></span><span id="_T"></span>**/t**  
データ型がわかっている場合、各シンボルのデータ型が表示されます。

<span id="_v"></span><span id="_V"></span>**/v**  
各シンボルの記号の型 (ローカル、グローバル、パラメーター、関数、または不明) が表示されます。 このオプションには、各シンボルのサイズも表示されます。 関数シンボルのサイズは、メモリ内の関数のサイズです。 その他の記号のサイズは、シンボルを表すデータ型のサイズです。 サイズは常にバイト単位で測定され、16 進数形式で表示されます。

<span id="_s_Size"></span><span id="_s_size"></span><span id="_S_SIZE"></span>**/s** *サイズ*  
値に表示されたシンボルのサイズ (バイト単位)、専用等しい*サイズ*します。 *サイズ*関数のシンボルはメモリ内の関数のサイズになります。 *サイズ*の他のシンボルがシンボルを表すデータ型のサイズ。 シンボルのサイズが決まることはできませんが常に表示されます。 *サイズ*0 以外の整数でなければなりません。

<span id="_q"></span><span id="_Q"></span>**/q**  
引用符で囲まれた形式で名前のシンボルが表示されます。

<span id="_p"></span><span id="_P"></span>**/p**  
デバッガーは関数名とその引数を表示するときに、かっこの前にスペースを省略します。 この種の表示が容易関数名、引数からコピーする場合、 **x**別の場所に表示します。

<span id="_f"></span><span id="_F"></span>**/f**  
関数のデータ サイズが表示されます。

<span id="_d"></span><span id="_D"></span>**/d**  
データのデータ サイズが表示されます。

<span id="_a"></span><span id="_A"></span>**/a**  
昇順のアドレスを指定して、表示を並べ替えます。

<span id="_A"></span><span id="_a"></span>**/A**  
表示をアドレス、降順で並べ替えます。

<span id="_n"></span><span id="_N"></span>**/n**  
表示を昇順での名前で並べ替えます。

<span id="_N"></span><span id="_n"></span>**/N**  
表示を降順での名前で並べ替えます。

<span id="_z"></span><span id="_Z"></span>**/z**  
表示サイズを昇順で並べ替えます。

<span id="_Z"></span><span id="_z"></span>**/Z**  
表示サイズを降順で並べ替えます。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
検索するモジュールを指定します。 このモジュールは、.exe、.dll、または .sys ファイルであることができます。 *モジュール*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *シンボル*   
シンボルを含める必要があるパターンを指定します。 *シンボル*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

照合が大文字小文字を区別し、1 つの先頭のアンダー スコアがないため、このパターンは、シンボルに一致すると、(\_) 任意の分量の先頭にアンダー スコアを表します。 内のスペースを追加することができます*シンボル*スペースが含まれるシンボル名を指定できるように、("operator new"などまたは"テンプレート&lt;A、B&gt;") せず、ワイルドカード文字を使用します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次のコマンドは、文字列「スピン」が含まれる MyModule ですべての記号を検索します。

```dbgcmd
0:000> x mymodule!*spin* 
```

次のコマンドは、すばやく MyModule 内"DownloadMinor"と"DownloadMajor"シンボルを検索します。

```dbgcmd
0:000> x mymodule!downloadm??or 
```

次のコマンドを使用して、MyModule ですべてのシンボルを表示することもできます。

```dbgcmd
0:000> x mymodule!* 
```

上記のコマンドもデバッガーに強制的に MyModule のシンボル情報を再読み込みします。 最小限のディスプレイを使用したモジュールのシンボルを再読み込みする場合は、次のコマンドを使用します。

```dbgcmd
0:000> x mymodule!*start* 
```

常に、いくつかのシンボルには、文字列"start"が含まれます。 そのため、上記のコマンドは、常にコマンドが動作を確認するには、いくつか出力を表示します。 上記のコマンドの過剰な表示の長さを回避できますが、* * x mymodule!\\***.

各シンボルは、完全なシンボル名の開始アドレスが表示されます。 シンボルが関数名の場合は、その引数の型の一覧は、表示も含まれます。 シンボルは、グローバル変数が、その現在の値が表示されます。

その他の 1 つの特殊なケースがある、 **x**コマンド。 アドレスとを現在のコンテキストのすべてのローカル変数の名前を表示するには、次のコマンドを使用します。

```dbgcmd
0:000> x * 
```

**注**  プライベート シンボルが読み込まれている場合を除き、ほとんどの場合、ローカル変数にアクセスすることはできません。 このような状況の詳細については、次を参照してください[dbgerr005:。プライベート シンボルのために必要な](dbgerr005--private-symbols-required.md)します。 ローカル変数の値を表示するには、使用、 [ **dv (ローカル変数の表示)** ](dv--display-local-variables-.md)コマンド。

 

次の例を示しています、 **/0**、 **/1**、および **/2**オプション。

```dbgcmd
0:000:x86> x /0 MyApp!Add*
00b51410          
00b513d0 
      
0:000:x86> x /1 MyApp!Add*
MyApp!AddThreeIntegers
MyApp!AddTwoIntegers

0:000:x86> x /2 MyApp!Add*
00b51410          MyApp!AddThreeIntegers
00b513d0          MyApp!AddTwoIntegers
```

**/0**、 **/1**、および **/2**オプションの出力を使用する場合に便利ですが、 **x**コマンドへの入力として、 [ **.foreach** ](-foreach.md)コマンド。

```dbgcmd
.foreach ( place { x /0 MyApp!*MySym*} ) { .echo ${place}+0x18 }
```

次の例では、スイッチ **/f**フィルター関数モジュール notepad.exe を使用する場合。

```dbgcmd
0:000> x /f /v notepad!*main*
prv func   00000001`00003340  249 notepad!WinMain (struct HINSTANCE__ *, struct HINSTANCE__ *, char *, int)
prv func   00000001`0000a7b0   1c notepad!WinMainCRTStartup$filt$0 (void)
prv func   00000001`0000a540  268 notepad!WinMainCRTStartup (void)
```

使用すると、 **/v**オプション、表示の最初の列 (ローカル、グローバル、パラメーター、関数、または不明) 記号の型を示しています。 2 番目の列は、シンボルのアドレスです。 3 番目の列は、(バイト単位)、記号のサイズです。 4 番目の列には、シンボル名とモジュールの名前が表示されます。 場合によっては、この表示の後に等号 (=) と記号のデータ型。 シンボル (パブリックまたは完全なシンボル情報) のソースが表示されます。

```dbgcmd
kd> x /v nt!CmType*
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 806c9e68  150 nt!CmTypeName = struct _UNICODE_STRING [42]
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 805bd7b0    0 nt!CmTypeString = unsigned short *[]
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

前の例では、データ型が 10 進形式で指定されたときに 16 進数形式で、サイズを指定します。 そのため、前の例の最後の行のデータ型は符号なし short 整数に 42 ポインターの配列が。 この配列のサイズは 42\*4 = 168 と 168 が 0xA8 と 16 進数形式で表示されます。

使用することができます、**/s * * * サイズ*シンボル (バイト単位)、サイズのものだけを表示するオプションは、特定の値。 たとえば、サイズが 0xA8 オブジェクトを表す記号を前の例のコマンドを制限できます。

```dbgcmd
kd> x /v /s a8 nt!CmType*
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

**データ型の使用**

**/T**オプションにより、デバッガーをそれぞれのシンボルのデータ型に関する情報を表示します。 多数のシンボルのこの情報が表示されていない場合にも、 **/t**オプション。 使用すると **/t**、このようなシンボルがあるそのデータ型情報を 2 回表示されます。

```dbgcmd
0:001> x prymes!__n*
00427d84 myModule!__nullstring = 0x00425de8 "(null)"
0042a3c0 myModule!_nstream = 512
Type information missing error for _nh_malloc
004021c1 myModule!MyStructInstance = struct MyStruct
00427d14 myModule!_NLG_Destination = <no type information>

0:001> x /t prymes!__n*
00427d84 char * myModule!__nullstring = 0x00425de8 "(null)"
0042a3c0 int myModule!_nstream = 512
Type information missing error for _nh_malloc
004021c1 struct MyStruct myModule!MyStructInstance = struct MyStruct
00427d14 <NoType> myModule!_NLG_Destination = <no type information>
```

X のコマンドは、型のインスタンスが表示されます。

```dbgcmd
0:001> x foo!MyClassInstance
00f4f354          foo!MyClassInstance = 0x00f78768
```

X のコマンドは、型の名前だけに基づくものにも表示されません。

```dbgcmd
0:001> x foo!MyClass
0:001>
```

型の名前を使用して型情報を表示するには、使用を検討して[ **dt (型の表示)**](dt--display-type-.md)型と型のインスタンスの両方の情報を提供します。

```dbgcmd
0:001> dt foo!MyClass
   +0x000 IntMemberVariable : Int4B
   +0x004 FloatMemberVariable : Float
   +0x008 BoolMemberVariable : Bool
   +0x00c PtrMemberVariable : Ptr32 MyClass
```

**テンプレートでの作業**

X コマンドでワイルドカードを使用して、このサンプルで示すように、テンプレート クラスを表示することができます。

```dbgcmd
0:001>  x Fabric!Common::ConfigEntry*TimeSpan?
000007f6`466a2f9c Fabric!Common::ConfigEntry<Common::TimeSpan>::ConfigEntry<Common::TimeSpan> (void)
000007f6`466a3020 Fabric!Common::ConfigEntry<Common::TimeSpan>::~ConfigEntry<Common::TimeSpan> (void)
```

使用を検討して、 [ **dt (型の表示)** ](dt--display-type-.md)コマンド、テンプレートを使用する場合、x コマンドでは個々 のテンプレート クラスの項目は表示されません。

```dbgcmd
0:001> dt foo!Common::ConfigEntry<Common::TimeSpan>
   +0x000 __VFN_table : Ptr64 
   +0x008 componentConfig_ : Ptr64 Common::ComponentConfig
   +0x010 section_         : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
   +0x038 key_             : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[シンボルを確認します。](verifying-symbols.md)

[**dv (ローカル変数の表示)**](dv--display-local-variables-.md)

 

 






