---
title: SymChk の使用
description: SymChk の使用
ms.assetid: 60c3df99-a842-4e46-a504-8e2b54030eef
keywords:
- SymChk を使用して
ms.date: 10/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de2c5a15563aa81d706f4b6bd0feb24b564c4fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579656"
---
# <a name="using-symchk"></a>SymChk の使用


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>

SymChk の基本構文は次のとおりです。

```console
symchk [/r] FileNames /s SymbolPath 
```

*ファイル名*のシンボルが必要な 1 つまたは複数のプログラム ファイルを指定します。 場合*ファイル名*ディレクトリと **/r**フラグが使用される、このディレクトリは再帰的に探索、および SymChk はすべてのプログラム ファイルがこのディレクトリ ツリー内のシンボルを検索しようとしています。 *SymbolPath* SymChk のシンボルの検索場所を指定します。

多くのコマンド ライン オプションがあります。 完全な一覧については、次を参照してください。 [SymChk コマンド ライン オプション](symchk-command-line-options.md)します。

### <a name="obtaining-symchk"></a>Symchk を取得します。

Symchk、他のデバッグ ツールなどには、デバッガーの一部として出荷されます。 詳細については、次を参照してください。[デバッグ ツールの Windows にダウンロード](debugger-download-tools.md)します。

デバッグ ツールがインストールされると、symchk は 64 ビット Windows の場合は、このディレクトリで使用できます。

C:\\プログラム ファイル (x86)\\Windows キット\\10\\デバッガー\\x64

### <a name="example-usage"></a>使用例

指定されたシンボル パスには、ローカルのディレクトリ、UNC ディレクトリ、またはシンボル サーバーの任意の数を含めることができます。 ローカル ディレクトリと UNC ディレクトリが再帰的に検索ではありません。 指定されたディレクトリだけと実行可能ファイルの拡張子に基づいたサブディレクトリが検索されます。 たとえば、クエリ

```console
symchk thisdriver.sys /s g:\symbols 
```

g: 検索\\mysymbols と g:\\mysymbols\\sys です。


シンボル パスの一部として、次の構文のいずれかを使用して、シンボル サーバーを指定できます。

```console
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

これは、シンボル サーバーを使用して、デバッガーのシンボル パスによく似ています。 詳細については、次を参照してください。[シンボル サーバーを使用して、シンボル ストア](symbol-stores-and-symbol-servers.md)します。

ダウン ストリームのストアを指定すると、SymChk がシンボル サーバーを検出、ダウン ストリームのストアに配置して、すべての有効なシンボル ファイルのコピーになります。 完全一致のみのシンボル ファイルは、ダウン ストリームにコピーされます。

SymChk は常に、シンボル サーバーのクエリを実行する前に、ダウン ストリームのストアを検索します。 したがって他のユーザーがシンボル ストアを管理するとき、ダウン ストリームのストアの使用に関する注意が必要です。 SymChk を 1 回実行するシンボル ファイルを見つけた場合は、ダウン ストリームのストアにコピーします。 実行する場合、SymChk もう一度これらのファイルが変更またはシンボル ストアで削除された後、SymChk は気付かないこのことから、ので、調査対象外観をそれ以上、ダウン ストリームのストアで検出されます。

**注**   SymChk は常に、シンボル サーバー DLL として SymSrv (Symsrv.dll) を使用します。 その一方で、デバッガーは、いずれかが使用可能な場合は、SymSrv 以外の DLL のシンボル サーバーを選択できます。 (SymSrv とは、Windows のツールをデバッグ パッケージに含まれるシンボル サーバーのことです)。
 

### <a name="span-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanspan-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanspan-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanusing-symchk-to-determine-whether-symbols-are-private-or-public"></a><span id="Using_SymChk_to_determine_whether_symbols_are_private_or_public"></span><span id="using_symchk_to_determine_whether_symbols_are_private_or_public"></span><span id="USING_SYMCHK_TO_DETERMINE_WHETHER_SYMBOLS_ARE_PRIVATE_OR_PUBLIC"></span>SymChk を使用して、シンボルはプライベートまたはパブリックであるかどうかを決定するには

シンボル ファイルがプライベートかパブリックかどうかを調べるには、 **/v**その SymChk 詳細出力を表示するためのパラメーター。 MyApp.exe と MyApp.pdb として、フォルダー c: と\\.sym となります 次のコマンドを入力します。

```console
symchk /v c:\\sym\\MyApp.exe /s c:\\sym**
```

MyApp.pdb にプライベート シンボルが含まれている場合、SymChk の出力は次のようになります。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - private symbols & lines
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

MyApp.pdb はパブリック シンボルのみが含まれる場合 SymChk の出力は次のようになります。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - public symbols
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

検索を制限するには、パブリック シンボル ファイルのみを検索するために使用して、 **s**オプションは、 **/s**パラメーター (**/ss**)。 MyApp.pdb に唯一のパブリック シンボルが含まれている場合、次のコマンドは、一致を検索します。 MyApp.pdb にプライベート シンボルが含まれている場合、一致するを検出されません。

```console
symchk /v c:\\sym\\MyApp.exe /ss c:\\sym
```

詳細については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

例をいくつか紹介します。 次のコマンドは、プログラムの Myapp.exe のシンボルを検索します。

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\applications 

SYMCHK: Myapp.exe           FAILED  - Myapp.pdb is missing

SYMCHK: FAILED files = 1
SYMCHK: PASSED + IGNORED files = 0
```

別のシンボル パスを使用して再実行することができます。

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

検索が成功したこの時間。 -Verbose オプションは使用されません SymChk はシンボルの検索に失敗した対象のファイルのみを一覧表示します。 このため、この例ではファイルが表示されません。 ここで 1 つのファイルがあるため、成功した検索が「成功」のカテゴリと、「失敗」のカテゴリで [なし] に表示されていることを確認できます。

プログラム ファイルには、実行可能コードが含まれていない場合は無視されます。 多くのリソース ファイルでは、この型です。

すべてのプログラム ファイルのファイルの名前を表示する場合は、使用、 **/v**詳細出力を生成するオプション。

```console
e:\debuggers> symchk /v f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: MyApp.exe           PASSED

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

次のコマンドは、膨大な数のシンボル サーバーで Windows のシンボルを検索します。 これにはさまざまな可能性のあるエラー メッセージがあります。

```console
e:\debuggers> symchk /r c:\windows\system32 /s srv*\\manysymbols\windows 

SYMCHK: msisam11.dll         FAILED  - MSISAM11.pdb is missing
SYMCHK: msuni11.dll          FAILED  - msuni11link.pdb is missing
SYMCHK: msdxm.ocx            FAILED  - Image is split correctly, but msdxm.dbg i
s missing
SYMCHK: expsrv.dll           FAILED  - Checksum doesn't match with expsrv.DBG
SYMCHK: imeshare.dll         FAILED  - imeshare.opt.pdb is missing
SYMCHK: ir32_32.dll          FAILED  - Built with no debugging information
SYMCHK: author.dll           FAILED  - rpctest.pdb is missing
SYMCHK: msvcrt40.dll         FAILED  - Built with no debugging information
......
SYMCHK: FAILED files = 211
SYMCHK: PASSED + IGNORED files = 4809
```

## <a name="see-also"></a>関連項目

[SymChk コマンド ライン オプション](symchk-command-line-options.md)

[シンボル サーバーとシンボル ストアを使用してください。](symbol-stores-and-symbol-servers.md)


 





