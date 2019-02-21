---
title: すべてのトレースの行にプレフィックスの出力を変更する方法
description: すべてのトレースの行にプレフィックスの出力を変更する方法
ms.assetid: be2b6207-79f5-4d71-a6a2-075f3078a873
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61becf5f3b8a75ee0541712cbc9a127ee8c7b462
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553866"
---
# <a name="how-do-i-change-the-prefix-output-on-every-trace-line"></a>すべてのトレースの行にプレフィックスの出力を変更する方法はありますか


すべてのトレースの行にプレフィックスの出力を変更するのにには、次のコマンドを使用します。

```
set TRACE_FORMAT_PREFIX=[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!] 
tracefmt -f mytracefile 
```

トレースについて\_形式\_パラメーターのプレフィックスを参照してください、[トレース メッセージのプレフィックス](trace-message-prefix.md)トピック。









