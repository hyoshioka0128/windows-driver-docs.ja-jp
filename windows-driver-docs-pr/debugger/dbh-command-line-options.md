---
title: DBH のコマンドライン オプション
description: DBH コマンドラインは、次の構文を使用します。
ms.assetid: fd333c2d-1f07-4a47-8653-e10cf58417a5
keywords:
- DBH コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DBH Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 482138a444fcc8780381ba7f8dee4a4f652398da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574560"
---
# <a name="dbh-command-line-options"></a>DBH のコマンドライン オプション


DBH コマンドラインは、次の構文を使用します。

```console
dbh [Options] -p:PID [Command] 

dbh [Options] ExecutableName [Command] 

dbh [Options] SymbolFileName [Command] 

dbh -? 

dbh -??  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="-p_PID"></span><span id="-p_pid"></span><span id="-P_PID"></span>**-p:**<em>PID</em>  
シンボルが読み込まれるプロセスのプロセス ID を指定します。

<span id="_______ExecutableName______"></span><span id="_______executablename______"></span><span id="_______EXECUTABLENAME______"></span> *ExecutableName*   
(通常、.exe または .sys) ファイル名拡張子を含むそのシンボルが読み込まれるには、実行可能ファイルを指定します。 相対または絶対ディレクトリ パスを含める必要があります。パスが含まれていない場合は、現在の作業ディレクトリが使用されます。 この場所で指定されたファイルが見つからない場合 DBH 検索を使用して**SymLoadModuleEx**します。

<span id="_______SymbolFileName______"></span><span id="_______symbolfilename______"></span><span id="_______SYMBOLFILENAME______"></span> *SymbolFileName*   
ファイル名拡張子 (.pdb ファイルまたは .dbg) を含むそのシンボルが読み込まれる、シンボル ファイルを指定します。 相対または絶対ディレクトリ パスを含める必要があります。パスが含まれていない場合は、現在の作業ディレクトリが使用されます。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせ。

<span id="-d"></span><span id="-D"></span>**-d**  
エラーの原因は、シンボルを検索し、シンボルを表示するときに使用される名前を装飾します。 このオプションを使用するときに[SYMOPT\_PUBLICS\_のみ](symbol-options.md#symopt-publics-only)、オンになってと両方 SYMOPT\_UNDNAME と SYMOPT\_自動\_PUBLICS がオフになります。 これは、発行コマンド symopt DBH を実行した後、symopt-10002 続けて +4000 と同じです。

<span id="-s_Path"></span><span id="-s_path"></span><span id="-S_PATH"></span>**-%s:**<em>パス</em>  
指定されたシンボル パスを設定*パス*値。

<span id="-n_"></span><span id="-N_"></span>**-n**   
オン*ノイズの多いシンボルの読み込み*します。 シンボルの検索に関する詳細情報が表示されます。 読み込まれると、各シンボル ファイルの名前が表示されます。 デバッガー シンボル ファイルを読み込むことができません、エラー メッセージが表示されます。 テキストには、.pdb ファイルのエラー メッセージが表示されます。 .Dbg ファイルのエラー メッセージ、エラー コードは、winerror.h ファイルで説明したの形式です。 便利な場合は、これらのメッセージの一部しますが、一部のシンボル ファイルが見つからないか照合できない理由を分析するのに役立ちます。 シンボル ヘッダー情報を回復するためだけにイメージ ファイルが読み込まれる場合にも表示されます。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
原因 DBH を実行するには、指定された実行*コマンド*、し、終了します。 可能なコマンドの一覧は、[DBH コマンド](dbh-commands.md)を参照してください。

<span id="_______-_______"></span> **-?**   
DBH コマンドラインのヘルプを表示します。

<span id="_______-________"></span> **-??**   
DBH コマンドラインのヘルプ テキストを表示し、すべて DBH コマンドの一覧を表示します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

DBH ツールの詳細については、[を使用して DBH](using-dbh.md)を参照してください。

 

 





