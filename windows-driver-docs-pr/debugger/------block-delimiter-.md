---
title: (ブロックの区切り記号)
description: デバッガー コマンド プログラム内のステートメントのブロックを囲む中かっこ () のペアが使用されます。
ms.assetid: 1391fa51-61ce-40e5-8bf5-b5a2215c2bd9
keywords:
- (ブロックの区切り記号)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Block Delimiter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f3cdd069ee946d32c692dbed305cd0ce3427b68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334865"
---
# <a name="--block-delimiter"></a>{} (ブロックの区切り記号)


中かっこのペア ( **{}** )、デバッガー コマンド プログラム内でステートメント ブロックを囲むために使用されます。

```dbgcmd
    Statements { Statements } Statements 
```

## <span id="ddk_token_block_delimiter_dbg"></span><span id="DDK_TOKEN_BLOCK_DELIMITER_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッガー コマンド プログラムとコントロールのフロー トークンについては、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

各ブロックが入力されると、ブロック内のすべてのエイリアスが評価されます。 ある時点でコマンド ブロック内でエイリアスの値を変更する場合は、そのポイント後のコマンドは使用しません新しいエイリアスの値下位ブロック内である場合を除いて。

各ブロックは、コントロール フロー トークンを使用して開始する必要があります。 エイリアスの評価の目的のブロックを作成する場合でをプレフィックスする必要があります、 [ **.block** ](-block.md)トークンです。

 

 





