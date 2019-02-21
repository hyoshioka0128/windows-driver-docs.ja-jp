---
title: .block
description: .Block トークンには; 操作は実行されません。ステートメントのブロックを導入するためだけに使用されます。
ms.assetid: 8f1ac6b5-fea5-4e3f-8d4c-5e0533722885
keywords:
- デバッグ .block Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .block
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e46ceb9218c59b605d7eb29ae2e14c486412cf8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558195"
---
# <a name="block"></a>.block


**.Block**アクションも実行せずトークンは、ステートメント ブロックを導入するためだけに使用されます。

```dbgcmd
    Commands ; .block { Commands } ; Commands 
```

## <span id="ddk_token_block_dbg"></span><span id="DDK_TOKEN_BLOCK_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

新しいブロックを使用してエイリアスを評価する方法については、次を参照してください。 [Using エイリアス](using-aliases.md)と[**として (設定の別名) として**](as--as--set-alias-.md)します。

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>注釈
-------

コマンドのブロックは中かっこで囲まれています。 各ブロックが入力されると、ブロック内のすべてのエイリアスが評価されます。 ある時点でコマンド ブロック内でエイリアスの値を変更する場合は、そのポイント後のコマンドは使用しません新しいエイリアスの値下位ブロック内である場合を除いて。

各ブロックは、コントロール フロー トークンを使用して開始する必要があります。 エイリアスの評価の目的のブロックを作成する場合でをプレフィックスする必要があります、 **.block**トークン、このトークンがあるないため影響以外に導入されるブロックを許可します。

 

 





