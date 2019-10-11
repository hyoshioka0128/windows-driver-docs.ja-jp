---
title: $ $ (コメント指定子)
description: コマンドの先頭に2つのドル記号 ($ $) が表示される場合、コメントがセミコロンで終了しない限り、その行の残りの部分はコメントとして扱われます。
ms.assetid: bafd5e97-d443-4bfc-b3ee-c2867ed139a2
keywords:
- コメントトークン ($ $)
- $ $ (コメント指定子) Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $$ (Comment Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d666b934c787f2f752bec83b97f9c4234db5a0f9
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038050"
---
# <a name="-comment-specifier"></a>$ $ (コメント指定子)


コマンドの先頭に2つのドル記号 ( **$$** ) が表示された場合、コメントがセミコロンで終了しない限り、その行の残りの部分はコメントとして扱われます。


   $ $ [任意のテキスト]


<a name="remarks"></a>コメント
-------

**@No__t-1**トークンは、他のデバッガーコマンドと同様に解析されます。 そのため、別のコマンドの後にコメントを作成する場合は、 **$$** トークンの前にセミコロンを付ける必要があります。

**@No__t-1**トークンを指定すると、行の末尾またはセミコロンが検出されるまで、テキストが無視されます。 セミコロンでコメントが終了します。セミコロンが標準コマンドとして解析された後のテキスト。 これは **\*** [(コメント行指定子)](----comment-line-specifier-.md)とは異なり、セミコロンが存在する場合でも、行の残りの部分はコメントになります。

たとえば、次のコマンドは、 **eax**と**ebx**を表示しますが、 **ecx**は表示しません。

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

**@No__t-1**または **$$** トークンがプレフィックスとして付けられたテキストは、何らかの方法で処理されません。 リモートデバッグを実行している場合、デバッグサーバーに入力したコメントは、デバッグクライアントでは表示されません。その逆も同様です。 すべてのパーティに表示されるように、デバッガーコマンドウィンドウにコメントテキストを表示する場合は、 [ **. echo (Echo comment)** ](-echo--echo-comment-.md)を使用する必要があります。
