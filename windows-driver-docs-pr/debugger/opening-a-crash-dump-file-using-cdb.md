---
title: CDB を使用してダンプ ファイルを開く
description: CDB を使用してダンプ ファイルを開く
ms.assetid: 204DFA6F-2BA2-4B76-AFE0-28207710322B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7bcc014ca2c85e294c2edc19a669d3ad175c40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553565"
---
# <a name="opening-a-dump-file-using-cdb"></a>CDB を使用してダンプ ファイルを開く


## <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>コマンド プロンプト


コマンド プロンプト ウィンドウで CDB を起動するときに、ユーザー モード ダンプ ファイルを開くことができます。 次のコマンドを入力します。

**cdb -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 コマンドライン構文の詳細については、次を参照してください[ **CDB コマンド ライン オプション。**](cdb-command-line-options.md)

## <a name="span-idcdbcommandlinespanspan-idcdbcommandlinespanspan-idcdbcommandlinespancdb-command-line"></a><span id="CDB_Command_Line"></span><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB コマンドライン


入力して、デバッガーを実行した後も、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)コマンドの後に[ **g (移動)** ](g--go-.md). これにより、同時に複数のダンプ ファイルをデバッグすることができます。

 

 





