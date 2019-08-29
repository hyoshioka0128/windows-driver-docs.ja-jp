---
title: x (シンボルの検証)
description: X コマンドは、指定されたパターンに一致するすべてのコンテキストのシンボルを表示します。
ms.assetid: 8c71c2ca-4a9d-43e4-91b3-f05b5475316d
keywords:
- x (シンボルの確認) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- x (Examine Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 126db6c7b4cfdad17a2c0826302a625f267e3485
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866766"
---
# <a name="x-examine-symbols"></a>x (シンボルの検証)


**X**コマンドは、指定されたパターンに一致するすべてのコンテキストのシンボルを表示します。

```dbgcmd
x [Options] Module!Symbol 
x [Options] *
```

## <a name="span-idddk_cmd_examine_symbols_dbgspanspan-idddk_cmd_examine_symbols_dbgspanparameters"></a><span id="ddk_cmd_examine_symbols_dbg"></span><span id="DDK_CMD_EXAMINE_SYMBOLS_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
シンボル検索オプションを指定します。 次のオプションの1つまたは複数を使用できます。

<span id="_0"></span> **/0**  
各記号のアドレスのみを表示します。

<span id="_1"></span> **/1**  
各記号の名前のみを表示します。

<span id="_2"></span> **</span>**  
各記号のアドレスと名前のみを表示します (データ型ではありません)。

<span id="_D"></span><span id="_d"></span>**D**  
[デバッガーマークアップ言語](debugger-markup-language-commands.md)を使用して出力を表示します。

<span id="_t"></span><span id="_T"></span> **/t**  
データ型がわかっている場合は、各シンボルのデータ型を表示します。

<span id="_v"></span><span id="_V"></span> **/v**  
各シンボルのシンボルの種類 (local、global、parameter、function、または unknown) を表示します。 このオプションでは、各記号のサイズも表示されます。 関数シンボルのサイズは、メモリ内の関数のサイズです。 その他の記号のサイズは、シンボルが表すデータ型のサイズです。 サイズは常にバイト単位で測定され、16進形式で表示されます。

<span id="_s_Size"></span><span id="_s_size"></span><span id="_S_SIZE"></span> **/s** *サイズ*  
サイズがバイト単位のシンボルだけが*サイズ*の値と等しい場合にのみ表示します。 関数シンボルの*サイズ*は、メモリ内の関数のサイズです。 その他の記号の*サイズ*は、シンボルが表すデータ型のサイズです。 サイズを特定できないシンボルは常に表示されます。 *サイズ*は0以外の整数である必要があります。

<span id="_q"></span><span id="_Q"></span> **/q**  
シンボル名を引用符で囲まれた形式で表示します。

<span id="_p"></span><span id="_P"></span> **/p**  
デバッガーが関数名とその引数を表示したときに、左中かっこの前のスペースを省略します。 このように表示されるのは、関数名と引数を**x**ディスプレイから別の場所にコピーする場合です。

<span id="_f"></span><span id="_F"></span> **/f**  
関数のデータサイズを表示します。

<span id="_d"></span><span id="_D"></span>**d**  
データのデータサイズを表示します。

<span id="_a"></span><span id="_A"></span> **/a**  
表示をアドレスで昇順に並べ替えます。

<span id="_A"></span><span id="_a"></span> **/A**  
表示をアドレスで降順に並べ替えます。

<span id="_n"></span><span id="_N"></span>**ms-dos**  
表示を名前で昇順に並べ替えます。

<span id="_N"></span><span id="_n"></span>**MS-DOS**  
表示を名前で降順に並べ替えます。

<span id="_z"></span><span id="_Z"></span> **/z**  
表示をサイズで昇順に並べ替えます。

<span id="_Z"></span><span id="_z"></span> **/Z**  
ディスプレイのサイズを降順で並べ替えます。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*モジュール*   
検索するモジュールを指定します。 このモジュールは、.exe、.dll、または .sys ファイルにすることができます。 *モジュール*には、さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、「[文字列ワイルドカード構文](string-wildcard-syntax.md)」を参照してください。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span>*シンボル*   
シンボルに含まれている必要があるパターンを指定します。 *シンボル*には、さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、「[文字列ワイルドカード構文](string-wildcard-syntax.md)」を参照してください。

このパターンがシンボルと一致するため、一致では大文字と小文字が区別されず\_、1つの先頭のアンダースコア () は先頭のアンダースコアの任意の数量を表します。 *シンボル*内にスペースを追加すると、ワイルドカード文字を使用せずに、スペースを含むシンボル名 ("operator new&lt;" や "&gt;Template A, B" など) を指定できるようになります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次のコマンドは、文字列 "spin" を含む MyModule 内のすべてのシンボルを検索します。

```dbgcmd
0:000> x mymodule!*spin* 
```

次のコマンドは、MyModule の "DownloadMinor" と "Downloadminor" の記号をすばやく検索します。

```dbgcmd
0:000> x mymodule!downloadm??or 
```

次のコマンドを使用して、MyModule 内のすべてのシンボルを表示することもできます。

```dbgcmd
0:000> x mymodule!* 
```

また、上記のコマンドは、MyModule からシンボル情報を再読み込みするようにデバッガーに強制します。 最小限の表示でモジュール内のシンボルを再読み込みする場合は、次のコマンドを使用します。

```dbgcmd
0:000> x mymodule!*start* 
```

いくつかの記号には、常に文字列 "start" が含まれています。 したがって、上記のコマンドは、コマンドが動作することを確認するために出力を常に表示します。 ただし、上記のコマンドでは、表示長が**x mymodule\*!** を超えないようにします。

表示には、各記号の開始アドレスと完全なシンボル名が表示されます。 シンボルが関数名の場合は、その引数の型のリストも表示されます。 シンボルがグローバル変数の場合は、その現在の値が表示されます。

**X**コマンドには、他にも特殊なケースが1つあります。 現在のコンテキストのすべてのローカル変数のアドレスと名前を表示するには、次のコマンドを使用します。

```dbgcmd
0:000> x * 
```

**メモプライベートシンボル**が読み込まれていない場合、ほとんどの場合、ローカル変数にアクセスすることはできません。   この状況の詳細については[、「dbgerr005:プライベートシンボルが](dbgerr005--private-symbols-required.md)必要です。 ローカル変数の値を表示するには、[ [**dv (ローカル変数の表示)** ](dv--display-local-variables-.md) ] コマンドを使用します。

 

次の例は、 **/0**、 **/1**、/ **2**の各オプションを示しています。

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

**/0**、 **/1**、 **/2**オプションは、 **x**コマンドの出力を[**foreach**](-foreach.md)コマンドへの入力として使用する場合に便利です。

```dbgcmd
.foreach ( place { x /0 MyApp!*MySym*} ) { .echo ${place}+0x18 }
```

次の例では、スイッチ **/f**を使用してモジュール notepad.exe の関数をフィルター処理する方法を示します。

```dbgcmd
0:000> x /f /v notepad!*main*
prv func   00000001`00003340  249 notepad!WinMain (struct HINSTANCE__ *, struct HINSTANCE__ *, char *, int)
prv func   00000001`0000a7b0   1c notepad!WinMainCRTStartup$filt$0 (void)
prv func   00000001`0000a540  268 notepad!WinMainCRTStartup (void)
```

**/V**オプションを使用すると、表示の最初の列にシンボルの種類 (local、global、parameter、function、または unknown) が表示されます。 2番目の列は、記号のアドレスです。 3番目の列は、記号のサイズ (バイト単位) です。 4番目の列には、モジュール名とシンボル名が表示されます。 場合によっては、この表示の後に等号 (=) が続き、その後に記号のデータ型が続きます。 シンボルのソース (パブリックまたは完全なシンボル情報) も表示されます。

```dbgcmd
kd> x /v nt!CmType*
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 806c9e68  150 nt!CmTypeName = struct _UNICODE_STRING [42]
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 805bd7b0    0 nt!CmTypeString = unsigned short *[]
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

前の例では、サイズは16進数形式で指定されていますが、データ型は10進数形式で指定されています。 このため、前の例の最後の行では、データ型は、符号なし short 整数への42ポインターの配列です。 この配列のサイズは 42\*4 = 168 で、168は、16進形式で0xa8 として表示されます。

* */S***size*オプションを使用すると、サイズが特定の値であるシンボル (バイト単位) のみを表示できます。 たとえば、前の例のコマンドを、サイズが0xA8 のオブジェクトを表すシンボルに制限することができます。

```dbgcmd
kd> x /v /s a8 nt!CmType*
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

**データ型の操作**

**/T**オプションを指定すると、デバッガーは各シンボルのデータ型に関する情報を表示します。 多くの記号については、この情報は **/t**オプションなしでも表示されることに注意してください。 **/T**を使用すると、このような記号のデータ型情報が2回表示されます。

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

X コマンドは、型のインスタンスを表示します。

```dbgcmd
0:001> x foo!MyClassInstance
00f4f354          foo!MyClassInstance = 0x00f78768
```

X コマンドでは、型の名前のみに基づいて何も表示されません。

```dbgcmd
0:001> x foo!MyClass
0:001>
```

型の名前を使用して型情報を表示するには、 [**dt (表示型)** ](dt--display-type-.md)の使用を検討してください。型の型とインスタンスの両方についての情報が提供されます。

```dbgcmd
0:001> dt foo!MyClass
   +0x000 IntMemberVariable : Int4B
   +0x004 FloatMemberVariable : Float
   +0x008 BoolMemberVariable : Bool
   +0x00c PtrMemberVariable : Ptr32 MyClass
```

**テンプレートの操作**

このサンプルで示すように、ワイルドカードと x コマンドを使用して、テンプレートクラスを表示できます。

```dbgcmd
0:001>  x Fabric!Common::ConfigEntry*TimeSpan?
000007f6`466a2f9c Fabric!Common::ConfigEntry<Common::TimeSpan>::ConfigEntry<Common::TimeSpan> (void)
000007f6`466a3020 Fabric!Common::ConfigEntry<Common::TimeSpan>::~ConfigEntry<Common::TimeSpan> (void)
```

テンプレートを操作するときは、[ [**dt (Display Type)** ](dt--display-type-.md) ] コマンドを使用することを検討してください。 x コマンドでは、個々のテンプレートクラス項目が表示されません。

```dbgcmd
0:001> dt foo!Common::ConfigEntry<Common::TimeSpan>
   +0x000 __VFN_table : Ptr64 
   +0x008 componentConfig_ : Ptr64 Common::ComponentConfig
   +0x010 section_         : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
   +0x038 key_             : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[検証 (シンボルを)](verifying-symbols.md)

[**dv (ローカル変数の表示)** ](dv--display-local-variables-.md)

 

 






