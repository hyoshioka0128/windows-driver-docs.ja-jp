---
title: アスタリスク コメント行の指定子
description: 場合は、コマンドの先頭にアスタリスクが後にセミコロンが表示される場合でも、行の残りの部分は、コメントとして扱われます。
ms.assetid: 46f68e92-0758-49f2-82bb-bc4d25ddb641
keywords:
- 行のコメント トークン
- コメント行指定子の Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Comment Line Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0a9a87651019cf4524a81039f36b2a6b0921c10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337073"
---
# <a name="-comment-line-specifier"></a>\* (コメント行の指定子)


場合、アスタリスク ( **\\** *) 文字は、コマンドの先頭に、後にセミコロンが表示される場合でも、行の残りの部分は、コメントとして扱われます。

```dbgcmd
    * [any text]
```

<a name="remarks"></a>注釈
-------

**\\** * トークンは、他のデバッガー コマンドのように解析します。 そのため、別のコマンドの後にコメントを作成する場合は、文字の前に、 **\\** * セミコロン トークンです。

**\\** * 場合でも、その後にセミコロンが表示されます、トークンは、無視する行の残りの部分になります。 これに対し[ **$$ (コメント指定子)** ](-----comment-specifier-.md)セミコロンで終了するコメントを作成することができます。

たとえば、次のコマンドが表示されます**eax**と**ebx**、なく**ecx**:

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

テキストが付いて、 **\\** * または[ **$$** ](-----comment-specifier-.md)トークンは任意の方法で処理されていません。 リモート デバッグを実行する場合、デバッグ サーバーで入力したコメントに表示されない、デバッグのクライアントもその逆もします。 コメント テキストを使用する必要がありますすべての関係者に表示されるようにデバッガー コマンド ウィンドウに表示する場合[ **.echo (エコー コメント)** ](-echo--echo-comment-.md)します。

 

 





