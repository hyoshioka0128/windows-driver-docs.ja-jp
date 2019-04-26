---
title: 配置ファイルの構文
description: 配置ファイルは、それを配置するファイルに関連付けられているクラスのサブディレクトリを決定する BinPlace を読み取るテキスト ファイルです。
ms.assetid: 49f58ed1-9a4d-4e3e-9248-eebd95271374
keywords:
- ファイルの構文のドライバーの開発ツールを配置します。
topic_type:
- apiref
api_name:
- Place File Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c01f47bb90f157ac4e2b411f006bf553ff4211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356316"
---
# <a name="place-file-syntax"></a>配置ファイルの構文


**注**配置済みファイルは廃止されましたとは使用できません。 .



配置ファイルは、それを配置するファイルに関連付けられているクラスのサブディレクトリを決定する BinPlace を読み取るテキスト ファイルです。

このファイルの名前とパスは、-p PlaceFile コマンド ライン パラメーターによって指定されます。 これを使用しない場合、既定値は\\ツール\\placefil.txt します。 配置ファイルには、任意の数の行のことができます。 各行には、ファイルとクラスのサブディレクトリが一覧表示します。 ファイルを一覧表示しても、何も操作 BinPlace は発生しません。 BinPlace が提供されるたびにではなく、コマンドライン上のファイル名かどうか、そのファイルが一覧表示を表示する場所ファイルを開くことはできます。 場合は、BinPlace はその特定のファイルの場所のファイルで指定されたクラスのサブディレクトリを使用します。

配置ファイルの各行には、同じ形式があります。

```

     FileName Class[:Class[...]   [ ; Comment ] 
```

配置ファイルの各行では、これらの規則に従います。

-   *FileName*フィールドは、行を開始する必要があります。
-   *FileName*と*クラス*フィールドは、1 つまたは複数のスペースで区切る必要があります。
-   セミコロンは、行の任意の場所が表示されたら、すべての右側にはコメントとして扱われます。
-   空白行とをセミコロンで始まるコメント行が許可されます。

*FileName*と*クラス*フィールドについて次のように、説明。

## <a name="span-idddkplacefilesyntaxtoolsspanspan-idddkplacefilesyntaxtoolsspanparameters"></a><span id="ddk_place_file_syntax_tools"></span><span id="DDK_PLACE_FILE_SYNTAX_TOOLS"></span>パラメーター


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
BinPlace で機能するファイルの名前を指定するフィールドです。 *ファイル名*ファイル名拡張子を含める必要がありますが、ファイルのパスを含めることはできません。 (ファイル パスは BinPlace コマンドラインで指定されます)。

<span id="_______Class______"></span><span id="_______class______"></span><span id="_______CLASS______"></span> *クラス*   
このファイルに使用されるクラスのサブディレクトリを指定するフィールドです。 しない限り、 **-y**または **-: DEST**コマンド ライン スイッチを使用する場合、BinPlace はクラスのサブディレクトリの追加のルート インストール先ディレクトリを実行して作成されるディレクトリにファイルを配置し、ファイルの種類のサブディレクトリを追加します。 参照してください[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)の完全な詳細情報。

*クラス*開始も円記号で終了する必要があります。 ディレクトリ名では、スペースを含めることはできません。 内で使用できる特殊な文字列がある、*クラス*値。 実行可能ファイルとシンボル ファイルの配置の文字列の結果は異なります。 次の表では、これらの文字列の結果を示します。

すべてのビルド。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">実行可能ファイルへの影響</th>
<th align="left">シンボル ファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>小売</strong></p></td>
<td align="left"><p>無視されます。 このディレクトリのレベルはスキップされます。</p></td>
<td align="left"><p>という名前のリテラル ディレクトリとして扱われます<strong>小売</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p></p>
X86 コンピューター: <strong>i386</strong>します。
Itanium ベースのコンピューターの場合。<strong>IA64</strong>します。
X64 ベースのコンピューターの場合。<strong>AMD64</strong>します。</td>
<td align="left"><p>無視されます。 このディレクトリのレベルはスキップされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>system</strong></p></td>
<td align="left"><p>なります<strong>system32</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>system16</strong></p></td>
<td align="left"><p>なります<strong>システム</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>windows</strong></p></td>
<td align="left"><p>"."無視されます。 このディレクトリのレベルはスキップされます。</p></td>
<td align="left"><p>シンボル パスが<strong>小売</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ドライバー</strong></p></td>
<td align="left"><p>なります<strong>system32 \drivers</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>drvetc</strong></p></td>
<td align="left"><p>なります<strong>system32\drivers\etc</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>config</strong></p></td>
<td align="left"><p>なります<strong>system32 \config</strong>します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



X86 ビルドします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">実行可能ファイルへの影響</th>
<th align="left">シンボル ファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>なります<strong>system32</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プリンター</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\drivers\w32x86</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\prtprocs\w32x86</strong>します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



AMD64 ビルド。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">実行可能ファイルへの影響</th>
<th align="left">シンボル ファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>"<strong>..</strong>"などのルート インストール先のディレクトリが C:\Binaries\Amd64 の場合は、ファイルが配置されます C:\Binaries。</p></td>
<td align="left"><p>1 つのディレクトリのシンボル パスが削除されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プリンター</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\drivers\w32amd64</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\prtprocs\w32amd64</strong>します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



IA64 ビルド。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">実行可能ファイルへの影響</th>
<th align="left">シンボル ファイルへの影響</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>"<strong>..</strong>"</p></td>
<td align="left"><p>1 つのディレクトリのシンボル パスが削除されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プリンター</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\drivers\w32ia64</strong>します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>なります<strong>system32\spool\prtprocs\w32ia64</strong>します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



明記されない限り、シンボル パスはパスの最初のディレクトリのみを含めるに切り捨てられます。 たとえば、x86 を移動する BinPlace を使用していた場合のターゲット クラスを含む Build.exe という名前のファイル**プリンター**、次のコマンド構文を使用する場合があります。

```
binplace -r BinaryRoot  -xa -s SymbolsDir1 -n SymbolsDir2 SourceFileLocation\build.exe
```

コマンドは、次の出力ツリーで結果になります。

```
<SymbolsDir1>\system32\exe\build.pdb
<SymbolsDir2>\system32\exe\build.pdb 
<BinaryRoot>\system32\spool\drivers\w32x86\build.exe 
```

AMD64、IA64 のビルドを使用して、 **hal** BinPlace 結果が期待どおりではないため、クラス注意が必要です。 たとえば、ルート インストール先のディレクトリが c:\\バイナリ\\Amd64 として指定、 **hal** c: クラス、ファイルが配置されます\\バイナリおよびプロセッサ固有のディレクトリではなくを意図していた可能性があります。

複数のインスタンスを含めることができます、ファイルを複数の場所に配置する場合は、*クラス*コロンで区切られました。 コロンのディレクトリとの間にスペースできないする必要があります。 次に、例を示します。

```
someprogram.exe   dir1\dir2\dir3:otherdir1\otherdir2   ; To two locations
```

<span id="_______Comment______"></span><span id="_______comment______"></span><span id="_______COMMENT______"></span> *コメント*   
BinPlace でセミコロンの後に任意のテキストは無視されます。









