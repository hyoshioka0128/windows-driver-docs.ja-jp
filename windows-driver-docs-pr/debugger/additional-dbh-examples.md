---
title: 追加 DBH 例
description: 追加 DBH 例
ms.assetid: 6db23b6b-e5da-4ea3-9f0a-ab42c0e712d7
keywords:
- DBH、シンボルを表示します。
- DBH、シンボルの装飾
- DBH、データ型
- DBH、虚数部のシンボル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21292ca6ed92b9fc419dae7231298ca630ca6183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557995"
---
# <a name="additional-dbh-examples"></a>追加 DBH 例


DBH プロンプトで実行できるコマンドの他の例を示します。

### <a name="span-iddisplayingprivatesymbolsandpublicsymbolsspanspan-iddisplayingprivatesymbolsandpublicsymbolsspandisplaying-private-symbols-and-public-symbols"></a><span id="displaying_private_symbols_and_public_symbols"></span><span id="DISPLAYING_PRIVATE_SYMBOLS_AND_PUBLIC_SYMBOLS"></span>プライベート シンボルとパブリック シンボルを表示します。

かどうか、ターゲットは、完全なシンボル ファイル、ファイルに 2 回各パブリック シンボルが表示されます。 パブリック シンボルの表で、プライベート シンボル データにします。 多くの場合、パブリック シンボル テーブル内のコピーには、さまざまな文字の装飾 (プレフィックス/サフィックス) が含まれています。 詳細については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

DBH には、プライベート シンボル データに、装飾なしのパブリック シンボル テーブルおよびデコレーションでパブリック シンボル テーブルは、このシンボルに関する情報を表示できます。 これはすべて次の 3 種類が表示されます、コマンドを使用して、 **addr 414fe0**たび。

初めてこの例では、このコマンドが表示されます DBH は、結果として得られる情報はプライベート シンボル データから取得するために、既定のシンボル オプションを使用します。 この情報が、関数のアドレス、サイズ、およびデータ型が含まれることに注意してください**fgets**します。 次に、コマンド symopt +4000 を使用、SYMOPT をオンにする\_PUBLICS\_専用オプションです。 これにより、プライベート シンボル データを無視する DBH のためと、 **addr 414fe0**コマンドを実行すると、2 回目、DBH、パブリック シンボル テーブルを使用して、および関数のサイズやデータの型情報が表示されない**fgets**. 最後に、コマンド symopt-2 を使用、SYMOPT をオフにする\_UNDNAME に装飾を含めるオプションと DBH の原因です。 ときに、 **addr 414fe0**この最終回実行には、関数の名前の装飾バージョン **\_fgets**します。

```dbgcmd
pid:4308 mod:TimeTest[400000]: addr 414fe0

fgets
   name : fgets
   addr :   414fe0
   size : 113
  flags : 0
   type : 7e
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 7d

pid:4308 mod:TimeTest[400000]: symopt +4000

Symbol Options: 0x10c13
Symbol Options: 0x14c13

pid:4308 mod:TimeTest[400000]: addr 414fe0

fgets
   name : fgets
   addr :   414fe0
   size : 0
  flags : 0
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 7f

pid:4308 mod:TimeTest[400000]: symopt -2

Symbol Options: 0x14c13
Symbol Options: 0x14c11

pid:4308 mod:TimeTest[400000]: addr 414fe0

_fgets
   name : _fgets
   addr :   414fe0
   size : 0
  flags : 0
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 7f 
```

-D コマンド ライン オプションを使用した場合、結果が、装飾のパブリック名の先頭からを表示がなります。

### <a name="span-iddeterminingthedecorationsofaspecificsymbolspanspan-iddeterminingthedecorationsofaspecificsymbolspandetermining-the-decorations-of-a-specific-symbol"></a><span id="determining_the_decorations_of_a_specific_symbol"></span><span id="DETERMINING_THE_DECORATIONS_OF_A_SPECIFIC_SYMBOL"></span>特定の記号の文字装飾を決定します。

DBH には、特定のシンボルの装飾を決定できます。 など、その装飾を指定する記号を必要とするプログラムと組み合わせて使用する場合に役立ちます。 [PDBCopy](pdbcopy.md)します。

たとえば、シンボル ファイルの mysymbols.pdb に非装飾名を持つ記号が含まれていることがわかって**MyFunction1**します。 装飾名を検索するには、次の手順を使用します。

最初に、-d コマンド ライン オプションを指定しない DBH を起動し、すべての情報は、パブリック シンボル テーブルから取得できるように symopt +4000 コマンドを使用します。

```console
C:\> dbh c:\mydir\mysymbols.pdb

mysymbols [1000000]: symopt +4000

Symbol Options: 0x10c13
Symbol Options: 0x14c13 
```

次に、使用、**名前**コマンドまたは**列挙**必要なシンボルのアドレスを表示するコマンド。

```dbgcmd
mysymbols [1000000]: enum myfunction1 

 index            address     name
   2ab            102cb4e :   MyFunction1
```

シンボルの装飾を表示するようになりました symopt-2 を使用し、使用、 **addr**コマンドには、この記号のアドレス。

```dbgcmd
mysymbols [1000000]: symopt -2

Symbol Options: 0x14c13
Symbol Options: 0x14c11

mysymbols [1000000]: addr 102cb4e

_MyFunction1@4
   name : _InterlockedIncrement@4
   addr :  102cb4e
   size : 0
  flags : 0
   type : 0
modbase :  1000000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 2ab  
```

シンボルの装飾名が、これがわかります **\_ MyFunction1@4**します。

### <a name="span-iddecodingsymboldecorationsspanspan-iddecodingsymboldecorationsspandecoding-symbol-decorations"></a><span id="decoding_symbol_decorations"></span><span id="DECODING_SYMBOL_DECORATIONS"></span>シンボルの装飾のデコード

**Undec** C++ シンボルの装飾の意味を表示するコマンドを使用できます。 次の例では、文字装飾にアタッチされていますか。\_@ C\_03GGCAPAJC@Sep? @ $AA がデコードされる文字列であることを示します。

```dbgcmd
dbh: undec ??_C@_03GGCAPAJC@Sep?$AA@

??_C@_03GGCAPAJC@Sep?$AA@ =
`string' 
```

次の例では、3 つの関数名は、プロトタイプを明らかにアタッチされている文字装飾をデコードします。

```dbgcmd
dbh: undec ?gcontext@@3_KA

?gcontext@@3_KA =
unsigned __int64 gcontext


dbh: undec ?pathcpy@@YGXPAGPBG1K@Z

?pathcpy@@YGXPAGPBG1K@Z =
void __stdcall pathcpy(unsigned short *,unsigned short const *,unsigned short const *,unsigned long)


dbh: undec ?_set_new_handler@@YAP6AHI@ZP6AHI@Z@Z

?_set_new_handler@@YAP6AHI@ZP6AHI@Z@Z =
int (__cdecl*__cdecl _set_new_handler(int (__cdecl*)(unsigned int)))(unsigned int) 
```

**Undec**コマンドでは、初期のアンダー スコア、プレフィックスについての情報は表示されません **\_ \_imp\_**、または末尾の"**@**<em>アドレス</em>"装飾、一般的に見られるを関数名に接続されています。

使用することができます、 **undec**コマンドに現在読み込まれているモジュール内のシンボルの名前だけでなく、任意の文字列。

### <a name="span-idsortingalistofsymbolsbyaddressspanspan-idsortingalistofsymbolsbyaddressspansorting-a-list-of-symbols-by-address"></a><span id="sorting_a_list_of_symbols_by_address"></span><span id="SORTING_A_LIST_OF_SYMBOLS_BY_ADDRESS"></span>アドレスでシンボルの一覧を並べ替える

アドレスの順序で並べ替え、記号の一覧を単に必要な場合で実行できます DBH バッチ モード、パイプに結果を**並べ替え**コマンド。 次のコマンドは、アドレスで、結果を並べ替えるために、アドレスの値は通常、各行の 18 の列に開始します。

```dbgcmd
dbh -p:4672 enum mymodule!* | sort /+18
```

### <a name="span-iddisplayingsourcelineinformationspanspan-iddisplayingsourcelineinformationspandisplaying-source-line-information"></a><span id="displaying_source_line_information"></span><span id="DISPLAYING_SOURCE_LINE_INFORMATION"></span>ソース行情報を表示します。

完全なシンボル ファイルを使用するとき、DBH はソース行情報を表示できます。 これは不要なソース ファイルへのアクセス シンボル ファイル自体にこの情報が格納されるためです。

ここでは、**行**コマンドは、指定したソース行に対応するバイナリの命令の 16 進数のアドレスを表示し、その行に関連付けられているシンボルが表示されます。 (この例ではありません、行に関連付けられているシンボル。)

```dbgcmd
dbh [1000000]: line myprogram.cpp#767

   file : e:\mydirectory\src\myprogram.cpp
   line : 767
   addr :  1006191
    key : 0000000000000000
disp : 0
```

ここでは、 **srclines**コマンドは、指定したソース行に関連付けられているオブジェクト ファイルを表示します。

```dbgcmd
dbh [1000000]: srclines myprogram.cpp 767

0x1006191: e:\mydirectory\objchk\amd64\myprogram.obj
line 767 e:\mydirectory\src\myprogram.cpp
```

なお、出力の**srclines**に似ていますが、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)デバッガー コマンド。

### <a name="span-iddisplayingadatatypespanspan-iddisplayingadatatypespandisplaying-a-data-type"></a><span id="displaying_a_data_type"></span><span id="DISPLAYING_A_DATA_TYPE"></span>データ型を表示します。

**型**データ型に関する情報を表示するコマンドを使用できます。 ここで CMDPROC 型に関するデータが表示されます。

```dbgcmd
dbh [1000000]: type CMDPROC

   name : CMDPROC
   addr :        0
   size : 8
  flags : 0
   type : c
modbase :  1000000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagTypedef (11)
  index : c
```

「タグ」は、このデータ型の性質を指定の後に表示する値。 この場合、 **SymTagTypedef**を使用してこの型が定義されたことを示します、 **typedef**ステートメント。

### <a name="span-idusingimaginarysymbolsspanspan-idusingimaginarysymbolsspanusing-imaginary-symbols"></a><span id="using_imaginary_symbols"></span><span id="USING_IMAGINARY_SYMBOLS"></span>虚数部のシンボルを使用します。

**追加**コマンドでは、虚数部のシンボルが読み込まれたモジュールを追加できます。 実際のシンボル ファイルは変更されません。DBH のメモリでそのファイルのイメージのみが変更されます。

**追加**コマンドをできるシンボルが特定のアドレス範囲に関連付けられた一時的に無効にする場合に便利です。 次の例では、アドレス範囲の一部の実行に関連付けられた**MyModule! メイン**虚数部の記号でオーバーライドされる**MyModule! マジック**します。

虚数部のシンボルを追加する前に、モジュールの表示方法を示します。 なお、**メイン**関数が 0x0042CC56 で開始し、サイズ 0x42B が。 したがって、 **addr** 0x0042CD10 アドレスを持つコマンドを使用すると、このアドレスの境界内にあるとして認識、**メイン**関数。

```dbgcmd
pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup

pid:6040 mod:MyModule[400000]: addr 42cc56

main
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1

pid:6040 mod:MyModule[400000]: addr 42cd10

main+ba
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1 
```

今すぐシンボル**マジック**0x0042CD00、0x10 のサイズ (バイト) でのアドレスに追加されます。 ときに、 **enum**コマンドを使用して、インデックスのビットを設定すると、虚数部のシンボルであるかを示します。

```dbgcmd
pid:6040 mod:MyModule[400000]: add magic 42cd00 10


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup
  80000001             42cd00 :   magic 
```

ときに、 **addr**コマンドを使用すると、その範囲が指定されたアドレスを含めるシンボルが検索されます。 0x004CD10 アドレスが関連付けられているようになりましたので、この検索は、指定したアドレスと旧バージョンとの実行で始まる、**マジック**します。 0x004CD40 アドレスがまだに関連付けられている一方で**メイン**の範囲の外側にあるため、**マジック**シンボル。 また、タグ**SymTagCustom**虚数部の記号を示します。

```dbgcmd
pid:6040 mod:MyModule[400000]: addr 42cd10

magic+10
   name : magic
   addr :   42cd00
   size : 10
  flags : 1000
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagCustom (1a)
  index : 80000001

pid:6040 mod:MyModule[400000]: addr 42cd40

main+ea
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1 
```

最後に、 **del**コマンドは、シンボルを削除できます**マジック**、それぞれの元の範囲にすべてのシンボルを返します。

```dbgcmd
pid:6040 mod:MyModule[400000]: del magic


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup 
```









