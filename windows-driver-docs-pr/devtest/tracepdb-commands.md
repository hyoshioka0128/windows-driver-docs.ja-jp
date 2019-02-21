---
title: Tracepdb コマンド
description: Tracepdb を使用するには、コマンド プロンプト ウィンドウで、コマンドを入力します。 次の構文には、Tracepdb コマンドの要素が表示されます。
ms.assetid: c6502f26-d50e-48dc-85b4-978a83abff33
keywords:
- Tracepdb は、ドライバー開発ツールをコマンドします。
topic_type:
- apiref
api_name:
- Tracepdb Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cbe1a056df14579548d49e3aacbc2c5d1f9d5e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535773"
---
# <a name="tracepdb-commands"></a>Tracepdb コマンド


Tracepdb を使用するには、コマンド プロンプト ウィンドウで、コマンドを入力します。 次の構文には、Tracepdb コマンドの要素が表示されます。

PDB ファイルの場所を指定するのにには、次のパラメーターを使用します。

```
    tracepdb [-f PDBFiles] [-s] [-p TMFDirectory] [-v] [-c]
```

イメージ ファイルを指定する、次のパラメーターを使用して、[トレース プロバイダー](trace-provider.md)します。

```
    tracepdb -i ImageFiles [-r SymbolPaths] [-p TMFDiretory]  [-v]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-f_______PDBfiles______"></span><span id="_______-f_______pdbfiles______"></span><span id="_______-F_______PDBFILES______"></span> **-f** *PDBfiles*   
Tracepdb への入力 PDB シンボル ファイルの場所を指定します。 既定値は\*ローカル ディレクトリに .pdb。

*PDBFiles*は PDB ファイルの 1 つまたは複数のパスとファイルの名前です。 ファイル名は、アスタリスクのワイルドカード文字を含めることができます (\*) 複数の文字と 1 つの文字を表す疑問符 (?) を表します。 セミコロン (;) の使用します。ファイル名を区切ります。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
再帰的に検索します。 TMF ファイルの値に一致するすべての PDB ファイルを作成、 **-f**ディレクトリとで指定されたパスのすべてのサブディレクトリ内のパラメーター、 **-f**パラメーター。 場合 **-f**を省略すると、 **-s**ローカル ディレクトリとそのサブディレクトリ内のすべての PDB ファイル TMF ファイルが作成されます。

<span id="_______-p_______TMFDirectory______"></span><span id="_______-p_______tmfdirectory______"></span><span id="_______-P_______TMFDIRECTORY______"></span> **-p** *TMFDirectory*   
Tracepdb を作成する TMF ファイルの場所を指定します。 既定では、ローカル ディレクトリです。

TMF ファイルは、Tracepdb 出力ファイルです。 TMF ファイルの名前を指定することはできません。 ファイル名は、 [GUID をメッセージ](message-guid.md)の[トレース プロバイダー](trace-provider.md)します。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span> **-i** *ImageFiles*   
イメージ ファイルの場所を指定します[トレース プロバイダー](trace-provider.md)ローカル コンピューター上です。 使用すると、 **-i**パラメーター、Tracepdb を使用してイメージ ファイルのバージョンと名前の PDB シンボル ファイルを検索します。

*画像ファイル*はパスと 1 つまたは複数のバイナリ ファイル (.exe、.dll、.sys) トレース プロバイダーのファイル名。 内のファイル名*の画像ファイル*などのワイルドカード文字を含めることができます\*(を複数の文字を表す) としますか? (を 1 つの文字を表す)。 セミコロンで区切ります (**;**) イメージ ファイル名を区切ります。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span> **-r** *SymbolPaths*   
PDB シンボル ファイルの場所を指定します。

*SymbolPaths*プライベート シンボルを格納するディレクトリまたはシンボル サーバー上のディレクトリに 1 つまたは複数のパスを表します。 内のパス名*SymbolPaths*などのワイルドカード文字を含めることができます\*(を複数の文字を表す) としますか? (を 1 つの文字を表す)。

含める場合は、 **-i**パラメーター、省略 **-r**、Tracepdb % で指定されたパス内の指定したイメージの PDB ファイルを検索\_NT\_シンボル\_%Path% 環境変数。 環境変数が設定されていない場合 Tracepdb が、既定のシンボル パスで検索**srv\*\\\\\\\\シンボル\\\\シンボル**.

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細な出力が表示されます。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
生成[TMC](trace-message-control-file.md)ファイル。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

```
tracepdb -v
tracepdb -f tracedrv.pdb
tracepdb -f c:\tracing\ndis*.pdb -s
tracepdb -f d:\tools\trace*.pdb -p d:\tracing
tracepdb -i d:\winddk\7060\src\general\tracing\tracedrv\objfre_wnet_x86_vh\tracedrv.sys -r 
tracepdb -i trace*.exe;flpy*.dll -p d:\tracing
tracepdb -i tracedrv.exe -r srv*\\\\symbolstore\\symbols\\new
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

TMF ファイルの名前は、 [GUID をメッセージ](message-guid.md)のソース ファイル。 ソース ファイルとファイルにトレース エントリ メッセージの GUID を表します。 Windows では、メッセージの GUID を使用して、トレース メッセージをメッセージの書式設定命令を含む TMF ファイルに関連付けます。

トレース書式命令にはが含まれていない PDB シンボル ファイルを送信すると、Tracepdb は情報メッセージが表示され、すべてのファイルは作成されません。

Tracefmt での PDB ファイルを指定されたパスを見つけられない場合は、コメントなしのコマンド プロンプトに戻ります。 処理の詳細を取得するコマンドを再送信、 **-v**パラメーター。









