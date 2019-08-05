---
title: パブリック シンボルとプライベート シンボル
description: パブリック シンボルとプライベート シンボル
ms.assetid: 61ed583d-8b97-4929-8d86-1a6353c13304
keywords:
- パブリック シンボル
- プライベート シンボル
- パブリック シンボル
- プライベート シンボル
- 製品版のシンボル
- シンボルをエクスポートします。
- シンボル ファイルを完全なシンボル ファイル
- シンボル ファイル、削除されたシンボル ファイル
- 完全なシンボル ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac67a9dad14bc4d34712c74c29861144592aff8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362388"
---
# <a name="public-and-private-symbols"></a>パブリック シンボルとプライベート シンボル


2 つの個別情報のコレクションが含まれています、フルサイズ .pdb ファイルまたは .dbg シンボル ファイルが、リンカーによって構築されると、:*プライベート シンボル データ*と*パブリック シンボル テーブル*します。 これらのコレクションが含まれている項目と各項目に関する情報を格納のリストが異なります。

プライベート シンボル データには、次のものが含まれています。

-   関数

-   グローバル変数

-   ローカル変数

-   ユーザー定義の構造体、クラス、およびデータ型に関する情報

-   ソース ファイルと各バイナリの命令に対応する、そのファイル内の行番号の名前

パブリック シンボル テーブルには、以下の項目が含まれます。

-   関数 (関数宣言を除く**静的**)

-   として指定されているグローバル変数**extern** (およびその他のグローバル変数の全オブジェクト ファイルが複数表示される)

一般的な規則としては、パブリック シンボル テーブルには別に 1 つのソース ファイルからアクセス可能である項目だけが含まれています。 1 つだけに表示される項目のオブジェクト ファイル--**静的**関数、1 つのソース ファイル内でのみはグローバル変数およびローカル変数はパブリック シンボル テーブルに含まれません。

これら 2 つのコレクションのデータ点が異なりますでどのような情報が含まれている項目ごとにします。 次の情報は通常プライベート シンボル データに含まれる各項目に含まれています。

-   項目の名前

-   仮想メモリ内の項目のアドレス

-   フレーム ポインターの省略 (FPO) レコードの各関数

-   各変数、構造、および関数のデータ型

-   型および関数の各パラメーターの名前

-   各ローカル変数のスコープ

-   各ソース ファイル内の各行に関連付けられているシンボル

その一方で、パブリック シンボル テーブルは、それに含まれる各項目に関する次の情報のみを格納します。

-   項目の名前。

-   そのモジュールの仮想メモリ空間内の項目のアドレス。 関数の場合は、これはそのエントリ ポイントのアドレスです。

-   各関数のフレーム ポインターの省略 (FPO) レコード。

つまり、パブリック シンボル データは 2 つの方法でプライベート シンボル データのサブセットとして: 項目の短い一覧が含まれており、各項目に関する以下の情報も含まれています。 たとえば、パブリック シンボル データでは、ローカル変数がまったく含まれませんしません。 それぞれのローカル変数は、アドレス、データ型、スコープと、プライベート シンボル データにのみ含まれます。 関数の場合はその一方で、プライベート シンボル データと、パブリック シンボル テーブルの両方に含まれますが、プライベート シンボル データには、関数名、アドレス、FPO レコード、入力パラメーターの名前と種類、および出力の種類が含まれているパブリック シンボル テーブルが含まれますだけ、関数名、アドレス、および FPO レコード。

プライベート シンボル データと、パブリック シンボル テーブルの他の 1 つの違いがあります。 名前を持つパブリック シンボル テーブル内の項目の多く*装飾*プレフィックスやサフィックスを使用します。 これらの装飾は、C コンパイラ、C++ コンパイラ、および MASM アセンブラーによって追加されます。 一般的なプレフィックスは、一連のアンダー スコアまたは文字列を含める **\_\_imp\_** (インポートした関数の指定)。 一般的なサフィックスは、アット マークから 1 つ以上を含める ( **@** ) の後にアドレスまたはその他の識別文字列。 これらの装飾は、関数名の可能性がありますまたはグローバル変数名は、さまざまなモジュールで繰り返される可能性があるため、シンボルを解消するために、リンカーによって使用されます。 これらの装飾には、パブリック シンボル テーブルにプライベート シンボル データのサブセットがある一般的な規則の例外です。

### <a name="span-idfull_symbol_files_and_stripped_symbol_filesspanspan-idfull_symbol_files_and_stripped_symbol_filesspanfull-symbol-files-and-stripped-symbol-files"></a><span id="full_symbol_files_and_stripped_symbol_files"></span><span id="FULL_SYMBOL_FILES_AND_STRIPPED_SYMBOL_FILES"></span>完全なシンボル ファイルと削除されたシンボル ファイル

A*完全なシンボル ファイル*プライベート シンボルのデータと、パブリック シンボル テーブルの両方が含まれています。 この種類のファイルとして呼ば、*プライベート シンボル ファイル*が、このようなファイルには、プライベートとパブリック両方の記号が含まれているは、この名前は、誤解を招く。

A*シンボル ファイルを除去*- パブリック シンボル テーブルのみを含む小さいファイルは、または場合によっては、パブリック シンボル テーブルのサブセットのみです。 このファイルとして呼ば、*パブリック シンボル ファイル*します。

### <a name="span-idcreating_full_and_stripped_symbol_filesspanspan-idcreating_full_and_stripped_symbol_filesspancreating-full-and-stripped-symbol-files"></a><span id="creating_full_and_stripped_symbol_files"></span><span id="CREATING_FULL_AND_STRIPPED_SYMBOL_FILES"></span>完全および削除されたシンボル ファイルを作成します。

Visual Studio でバイナリをビルドする場合は、いずれかの完全なまたは削除されたシンボル ファイルを作成できます。 バイナリの「デバッグ ビルド」を作成するときに Visual Studio では完全なシンボル ファイルを通常作成します。 シンボル ファイルはありませんが、完全作成または除去は、通常、"製品版ビルド"、Visual Studio を構築するときは、適切なオプションが設定されている場合にシンボル ファイルが作成されます。

ビルド ユーティリティを使用したバイナリをビルドする場合、このユーティリティは完全なシンボル ファイルを作成します。

BinPlace ツールを使用して、完全なシンボル ファイルから削除されたシンボル ファイルを作成できます。 最も一般的な BinPlace オプションを使用する場合 ( **--x-s n**)、削除されたシンボル ファイルは、後に表示されているディレクトリに、 **-s**スイッチ、および完全なシンボル ファイルがディレクトリに配置後に記載されている、 **-n**スイッチします。 BinPlace では、シンボル ファイルを削除、削除された、完全なバージョンのファイルは、同じシグネチャとその他の識別情報提供されます。 これにより、デバッグにいずれかのバージョンを使用することができます。

PDBCopy ツールを使用してファイルを作成、削除されたシンボル完全なシンボル ファイルからプライベート シンボル データを削除することで。 PDBCopy はパブリック シンボル テーブルの指定したサブセットを削除することもできます。 詳細については、次を参照してください。 [PDBCopy](pdbcopy.md)します。

SymChk ツールを使用して、シンボル ファイルがプライベート シンボルを含むかどうかを判断できます。 詳細については、次を参照してください。 [SymChk](symchk.md)します。

### <a name="span-idviewing_public_and_private_symbols_in_the_debuggerspanspan-idviewing_public_and_private_symbols_in_the_debuggerspanviewing-public-and-private-symbols-in-the-debugger"></a><span id="viewing_public_and_private_symbols_in_the_debugger"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_IN_THE_DEBUGGER"></span>デバッガーでパブリックおよびプライベート シンボルの表示

WinDbg、KD、CDB を使用するには、シンボルを表示します。 完全なシンボル ファイルにアクセスできる次のデバッガーのいずれかの場合、プライベート シンボル データに表示される情報と、パブリック シンボルの表に示す情報の両方があります。 プライベート シンボル データより詳細については、パブリック シンボル データにシンボルの装飾が含まれています。

プライベート シンボルへのアクセス、プライベート シンボル データはパブリック シンボル テーブルにこれらのシンボルが含まれていないため、常に使用します。 これらのシンボルが装飾することはありません。

パブリック シンボルにアクセスするとき、デバッガーの動作が特定の依存[シンボル オプション](symbol-options.md):

-   ときに、 [SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)オプションは、装飾は、パブリック シンボルの名前が表示されるときに含まれません。 さらに、シンボルを検索する場合、装飾は無視されます。 このオプションがオフの場合は、パブリック シンボルを表示するときに、装飾は表示されるされ、検索で装飾が使用されます。 プライベート シンボルは、どのような状況で装飾することはありません。 このオプションは、すべてのデバッガーで既定でオンです。

-   ときに、 [SYMOPT\_PUBLICS\_のみ](symbol-options.md#symopt-publics-only)オプションがオンで、プライベート シンボル データを無視すると、され、パブリック シンボル テーブルのみが使用されます。 このオプションは既定ではすべてのデバッガーではオフです。

-   ときに、 [SYMOPT\_いいえ\_PUBLICS](symbol-options.md#symopt-no-publics)オプションがオン、パブリック シンボル テーブルは無視され、検索およびシンボル情報だけでプライベート シンボル データを使用します。 このオプションは既定ではすべてのデバッガーではオフです。

-   ときに、 [SYMOPT\_自動\_PUBLICS](symbol-options.md#symopt-auto-publics)オプションがオン (両方 SYMOPT と\_PUBLICS\_のみと SYMOPT\_いいえ\_PUBLICS がオフになって)、最初のシンボルプライベート シンボル データに検索されます。 必要なシンボルは、そこで見つかった場合は、検索が終了します。 それ以外の場合は、パブリック シンボル テーブルが検索されます。 パブリック シンボル テーブルには、プライベート データ内のシンボルのサブセットが含まれている、ため通常この結果、パブリック シンボル テーブルは無視されます。

-   ときに、SYMOPT\_PUBLICS\_のみ、SYMOPT\_いいえ\_PUBLICS、および SYMOPT\_自動\_PUBLICS オプションがすべて無効には、プライベート シンボル データと、パブリック シンボル テーブルの両方がそれぞれ検索シンボルが必要な時間。 ただし、両方の場所で一致が見つかったプライベート シンボル データの一致が使用されます。 したがって、このインスタンスでの動作では場合と同じ SYMOPT\_自動\_SYMOPT を使用する点を除いて、PUBLICS は\_自動\_PUBLICS 少し早くにシンボルの検索条件が発生する可能性があります。

例を次に示しますコマンド[ **(シンボルを調べる) x** ](x--examine-symbols-.md) 3 回使用されています。 最初の時間は、既定のシンボルのオプションが使用され、プライベート シンボル データから情報を取得するため。 配列のアドレス、サイズ、およびデータ型に関する情報を含むことに注意してください**typingString**します。 次にのコマンド .symopt + 4000 が使用されて、デバッガーがプライベート シンボル データを無視します。 ときに、 **x**コマンドは、もう一度実行して、パブリック シンボル テーブルを使用し、この時間のサイズとデータの型情報はありませんは**typingString**します。 最後に、コマンド .symopt-2 が使用される、これにより、デバッガーに装飾を含めます。 ときに、 **x**コマンドは、この最後に、関数の名前の装飾のバージョンを実行 **\_typingString**が表示されます。

```dbgcmd
0:000> x /t /d *!*typingstring* 
00434420 char [128] TimeTest!typingString = char [128] ""

0:000> .symopt+ 4000

0:000> x /t /d *!*typingstring* 
00434420 <NoType> TimeTest!typingString = <no type information>

0:000> .symopt- 2

0:000> x /t /d *!*typingstring* 
00434420 <NoType> TimeTest!_typingString = <no type information> 
```

### <a name="span-idviewing_public_and_private_symbols_with_the_dbh_toolspanspan-idviewing_public_and_private_symbols_with_the_dbh_toolspanviewing-public-and-private-symbols-with-the-dbh-tool"></a><span id="viewing_public_and_private_symbols_with_the_dbh_tool"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_WITH_THE_DBH_TOOL"></span>パブリックおよびプライベート シンボルの DBH ツールを使用して表示します。

シンボルを表示する別の方法を使用して、 [DBH ツール](dbh.md)します。 DBH は、デバッガーと同じシンボル オプションを使用します。 DBH のまま、デバッガーのような[SYMOPT\_PUBLICS\_のみ](symbol-options.md#symopt-publics-only)と[SYMOPT\_いいえ\_PUBLICS](symbol-options.md#symopt-no-publics)に、既定でオフ[SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)と[SYMOPT\_自動\_PUBLICS](symbol-options.md#symopt-auto-publics)で既定では。 コマンド ライン オプションまたは DBH コマンドによって、これらの既定値をオーバーライドできます。

例を次に示します DBH コマンド**addr 414fe0** 3 回使用されています。 最初の時間は、既定のシンボルのオプションが使用され、プライベート シンボル データから情報を取得するため。 関数のアドレス、サイズ、およびデータの種類に関する情報を含むことに注意してください**fgets**します。 次に、コマンド symopt +4000 を使用すると、それが原因で DBH プライベート シンボル データを無視します。 ときに、 **addr 414fe0**が再度実行、公開はシンボル テーブルが使用されます。 この時間関数のサイズとデータの型情報がない**fgets**します。 最後に、コマンド symopt-2 が使用される、文字装飾を含める DBH を停止します。 ときに、 **addr 414fe0**は、この最後に、関数の名前の装飾のバージョンを実行 **\_fgets**が表示されます。

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

 

 





