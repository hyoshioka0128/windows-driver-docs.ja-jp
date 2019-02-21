---
title: '#SetPPPrefix プリプロセッサ ディレクティブ'
description: '#SetPPPrefix プリプロセッサ ディレクティブ'
ms.assetid: 3520aa66-1090-40db-9c9f-cfba0e6e2bee
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- SetPPPrefix ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c33caffc8f45a09f26373590c2be8c0cf9510409
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557843"
---
# <a name="setppprefix-preprocessor-directive"></a>\#SetPPPrefix プリプロセッサ ディレクティブ


```GDL
#SetPPPrefix: prefix
```

\#SetPPPrefix ディレクティブにより、*プレフィックス*現在プリプロセッサ プレフィックスの値します。 *プレフィックス*トークン値を指定でき、必要です。

同じプレフィックスを 2 回以上定義できます。 プレフィックスは、ディレクティブがありません-する--を処理する既存のデータから明確に識別するため、ユーザーが選択できます。 次のコード例では、通常 GDL エントリには、実際のディレクティブで混乱する可能性があります値が含まれている場合は、プレフィックスを変更する方法を示します。

```GDL
*%  assume current prefix is #
#SetPPPrefix: #Temp#
#Temp#Ifdef:  WINNT_60
*InfoMessage: "Use the Preprocessor Directive
#PreCompiled to make your GDL file sharable."
#Temp#Endif:  WINNT_60
#Temp#UndefinePrefix
*%  now back to normal # prefix.
```
