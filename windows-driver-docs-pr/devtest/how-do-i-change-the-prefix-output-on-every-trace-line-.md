---
title: すべてのトレースの行にプレフィックスの出力を変更する方法
description: すべてのトレースの行にプレフィックスの出力を変更する方法
ms.assetid: be2b6207-79f5-4d71-a6a2-075f3078a873
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61becf5f3b8a75ee0541712cbc9a127ee8c7b462
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360388"
---
# <a name="how-do-i-change-the-prefix-output-on-every-trace-line"></a>すべてのトレース行でプレフィックス出力を変更する方法


すべてのトレースの行にプレフィックスの出力を変更するのにには、次のコマンドを使用します。

```
set TRACE_FORMAT_PREFIX=[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!] 
tracefmt -f mytracefile 
```

トレースについて\_形式\_パラメーターのプレフィックスを参照してください、[トレース メッセージのプレフィックス](trace-message-prefix.md)トピック。









