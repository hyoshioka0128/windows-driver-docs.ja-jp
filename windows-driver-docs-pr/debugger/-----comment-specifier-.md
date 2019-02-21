---
title: $ (コメント指定子)
description: コマンドの先頭の 2 つのドル記号 ($$) が表示される場合、は、コメントは、セミコロンで終了していない限り、行の残りの部分が、コメントに扱われます。
ms.assetid: bafd5e97-d443-4bfc-b3ee-c2867ed139a2
keywords:
- コメント トークン ($$)
- $ (コメント指定子) の Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $$ (Comment Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 63a5e0bd2db2ac7f6831b8023fcff2442d4f5217
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551513"
---
# <a name="-comment-specifier"></a>$ (コメント指定子)


2 つのドルに署名する場合 ( **$$** )、コメントは、セミコロンで終了していない限り、行の残りの部分は、コメントとして扱われますし、コマンドの先頭に表示されます。


   $$ [テキスト]


<a name="remarks"></a>注釈
-------

**$$** トークンは、他のデバッガー コマンドのように解析します。 そのため、別のコマンドの後にコメントを作成する場合は、文字の前に、 **$$** トークンをセミコロンで区切ります。

**$$** トークンは、後にセミコロンが出現するまでまたは行の末尾まで無視されます。 セミコロンは、コメントを終了しますセミコロンは、標準のコマンドとして解析後のテキスト。 これに対し[  **\* (コメント行の指定子)**](----comment-line-specifier-.md)、これにより、行の残りの部分、コメント、セミコロンが存在する場合でもです。

たとえば、次のコマンドが表示されます**eax**と**ebx**、なく**ecx**:

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

テキストが付いて、 [ **\\** * ](----comment-line-specifier-.md)または**$$** トークンは任意の方法で処理されていません。 リモート デバッグを実行する場合、デバッグ サーバーで入力したコメントに表示されない、デバッグのクライアントもその逆もします。 コメント テキストを使用する必要がありますすべての関係者に表示されるようにデバッガー コマンド ウィンドウに表示する場合[ **.echo (エコー コメント)**](-echo--echo-comment-.md)します。

 

 





