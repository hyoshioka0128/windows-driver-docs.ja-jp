---
title: .catch
description: .Catch トークンは、プログラムが、エラーが発生した場合に終了するを防ぐために使用されます。C++ では、catch キーワードのように動作しません。
ms.assetid: cda195d8-c0b8-4fb2-99a8-e2e8d338482b
keywords:
- デバッグ .catch Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .catch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25eb75dc00c119855f41f58ea0f7f115665e12e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578411"
---
# <a name="catch"></a>.catch


**.Catch**トークンは、プログラムが、エラーが発生した場合に終了するを防ぐために使用されます。

ように動作しない、**キャッチ**C++ のキーワード。

```dbgsyntax
    Commands ; .catch { Commands } ; Commands 
```

## <span id="ddk_token_catch_dbg"></span><span id="DDK_TOKEN_CATCH_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

**.Catch**トークンの 1 つまたは複数のコマンドを囲む中かっこが続きます。

内でのコマンドの場合、 **.catch**ブロックがエラーを生成、エラー メッセージが表示されます、中かっこ内の残りのすべてのコマンドは無視されます、および右中かっこの後に最初のコマンドの実行が再開されます。

場合 **.catch**が使用されていない、エラーで、全体のデバッガー コマンド プログラムは終了します。

使用することができます[ **.leave** ](-leave.md)を終了する、 **.catch**ブロックします。

 

 





