---
title: KD を使用してダンプ ファイルを開く
description: KD を使用してダンプ ファイルを開く
ms.assetid: 458E9BA6-6FA0-4FEF-93A0-062C9E11D21F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcca62c84df3552034f3240a783ca4e7a10e977d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385038"
---
# <a name="opening-a-dump-file-using-kd"></a>KD を使用してダンプ ファイルを開く


## <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>コマンド プロンプト


コマンド プロンプト ウィンドウで、KD を起動するときにダンプ ファイルを開くことができます。 次のコマンドを使用します。

**kd -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 コマンドライン構文の詳細については、次を参照してください。 [ **KD コマンド ライン オプション**](kd-command-line-options.md)します。

## <a name="span-idkdcommandlinespanspan-idkdcommandlinespanspan-idkdcommandlinespankd-command-line"></a><span id="KD_Command_Line"></span><span id="kd_command_line"></span><span id="KD_COMMAND_LINE"></span>KD コマンドライン


入力して、デバッガーを実行した後も、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)コマンドの後に[ **g (移動)** ](g--go-.md).

 

 





