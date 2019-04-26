---
title: コマンド ラインからの BinPlace の使用
description: コマンド ラインからの BinPlace の使用
ms.assetid: ed92fee5-d45c-437a-8c3f-de51b910c2ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12c5fdb3b54fa7e01b969518a56bb614e679d242
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341636"
---
# <a name="using-binplace-from-the-command-line"></a>コマンド ラインからの BinPlace の使用


**重要な**  このトピックの例で、BINPLACE の使用方法の説明\_PLACEFILE マクロと[BinPlace](binplace.md)[**場所ファイル**](place-file-syntax.md). このマクロとファイルは、Windows 7 バージョンの Windows ドライバー キットの廃止と WDK の将来のバージョンではサポートされない可能性があります。

 

このトピックでは、コマンドラインから BinPlace の使用例を示します。

最初に、次のように、ルート インストール先ディレクトリを設定できます。

```
set _NTTREE=d:\ProjectRoot
```

次のように、配置ファイルのパスとファイル名を設定できます。

```
set BINPLACE_PLACEFILE=d:\mystuff\myplacefile.txt
```

ファイル d: の内容をできるように\\mystuff\\myplacefile.txt がようになります。

```
; This is a simple place file.
commonmodule.dll   retail
application.exe    files\bin
mydriver.sys       *\drivertree
extra.cab          appendix
```

これで次のコマンドで BinPlace を実行できます。

```
binplace g:\somelocation\extra.cab
```

Extra.cab、実行可能ファイルではないため BinPlace はだけ移動されます。 ルートのインストール先ディレクトリが d:\\projectroot します。 として配置ファイルにこのファイルのクラス ディレクトリが指定されて**付録**します。 ファイルの種類のサブディレクトリは、cab (移動されるファイルのファイル名拡張子) です。 Location d: にこのファイルをコピーするために、\\projectroot\\付録\\cab\\extra.cab します。

BinPlace を使用して、実行可能ファイルとそのシンボル ファイルのようになりました。 これを行うには、実行可能ファイル名を指定する--BinPlace が関連付けられているシンボル ファイルを検索します。

BinPlace に、実行可能ファイル名を渡すと、その実行可能ファイルと同じディレクトリには、そのシンボル ファイルが検索されます。 は、実行可能ファイルに格納されている CodeView レコードを読み取ることによって検出されない場合にある、そのレコードでは、シンボル ファイルのパスを見つけた場合は、そのパス内のシンボル ファイルを探します。

**注**   BinPlace の移動、処理できませんだけではシンボル ファイルの名前を明示的に指定する場合。

 

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\application.exe
```

実行可能ファイルは前に、と同じルート先ディレクトリを使用します。 そのクラスのディレクトリは、files\\bin です。 したがって、d: に配置されて\\projectroot\\ファイル\\bin\\application.exe します。

シンボル ファイルは、2 つの場所に配置されます。 (プライベートとパブリック両方のシンボルを含む) 完全なシンボル ファイルが g:\\完全\\ファイル\\bin\\exe\\application.pdb します。 (パブリック シンボルのみを含む)、削除されたシンボル ファイルが d: に\\除去\\ファイル\\bin\\exe\\application.pdb します。

ここで、commonmodule.dll で同様のコマンドを使用します。

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\commonmodule.dll
```

今回は、クラスのサブディレクトリは**小売**します。 実行可能ファイルをこのディレクトリ名は"クラスのサブディレクトリを使用しない のコードを d: に配置されているように\\projectroot\\application.exe します。 G: にシンボル ファイルを配置\\完全\\小売\\dll\\application.pdb と d:\\除去\\小売\\dll\\application.pdb します。

最後に、mydriver.sys で BinPlace を使用し、省略、 **-n**スイッチします。

```
binplace -a -x -s d:\stripped g:\builddir\mydriver.sys
```

ここでは、クラスのサブディレクトリ **\*/drivertree**します。 実行可能ファイル、アスタリスク (\*) は、プロセッサの種類に置き換えられます。 X86 を実行するいると仮定すると、実行可能ファイル、コンピューターを配置 d:\\projectroot\\i386\\drivertree\\application.exe します。 G: で、削除されたシンボル ファイルが配置されます\\完全\\drivertree\\sys\\application.pdb、シンボル ファイルにアスタリスクが無視されるためです。 **-N**スイッチを省略した場合、完全なシンボル ファイルが任意の場所に配置することはできません。

 

 





