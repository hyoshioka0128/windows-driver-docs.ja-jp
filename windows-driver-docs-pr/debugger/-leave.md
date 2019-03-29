---
title: .leave
description: .Leave トークンは .catch ブロックを終了するために使用します。
ms.assetid: 82c5cbf7-bccd-4abf-b52a-2db65e0a0c2c
keywords:
- デバッグ .leave Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .leave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69d8cb0cd70f3e5a85da8b9894c74b9aa371c110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579931"
---
# <a name="leave"></a>.leave


**.Leave**トークンからの終了を使用して、 [ **.catch** ](-catch.md)ブロックします。

```dbgcmd
.catch { ... ; .if (Condition) .leave ; ... } 
```

## <span id="ddk_token_leave_dbg"></span><span id="DDK_TOKEN_LEAVE_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

ときに、 **.leave**内でトークンが見つかる、 [ **.catch** ](-catch.md)ブロック、ブロック、および最初のコマンドの実行が再開されますから、プログラムが終了中かっこの後にします。

C と同じコントロール フロー トークンがないため**goto**ステートメントでは、通常使用する、 **.leave**内でトークンを[ **.if** ](-if.md)条件では、上記の構文の例で示すようにします。 ただし、これは実際に必要ではありません。

 

 





