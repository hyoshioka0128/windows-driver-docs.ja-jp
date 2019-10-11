---
title: アスタリスク文字のコメント行指定子
description: アスタリスク文字がコマンドの先頭にある場合、その後にセミコロンがある場合でも、行の残りの部分はコメントとして扱われます。
ms.assetid: 46f68e92-0758-49f2-82bb-bc4d25ddb641
keywords:
- コメント行トークン
- コメント行指定子 Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Comment Line Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3572a854051b602196009ec38d74ed1c2d0e0d19
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038043"
---
# <a name="-comment-line-specifier"></a>\* (コメント行指定子)

アスタリスク ( **\*** ) 文字がコマンドの先頭にある場合、その後にセミコロンがある場合でも、行の残りの部分はコメントとして扱われます。

```dbgcmd
    * [any text]
```

<a name="remarks"></a>コメント
-------

**@No__t-1**トークンは、他のデバッガーコマンドと同様に解析されます。 そのため、別のコマンドの後にコメントを作成する場合は、 **\*** トークンの前にセミコロンを付ける必要があります。

**@No__t-1**トークンを指定すると、その後にセミコロンがある場合でも、行の残りの部分は無視されます。 これは、セミコロンで終了できるコメントを作成する[ **$ $ (コメント指定子)** ](-----comment-specifier-.md)とは異なります。

たとえば、次のコマンドは、 **eax**と**ebx**を表示しますが、 **ecx**は表示しません。

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx
```

**@No__t-1**または[ **$$** ](-----comment-specifier-.md)トークンがプレフィックスとして付けられたテキストは、何らかの方法で処理されません。 リモートデバッグを実行している場合、デバッグサーバーに入力したコメントは、デバッグクライアントでは表示されません。その逆も同様です。 すべてのパーティに表示されるように、デバッガーコマンドウィンドウにコメントテキストを表示する場合は、 [ **. echo (Echo comment)** ](-echo--echo-comment-.md)を使用する必要があります。
