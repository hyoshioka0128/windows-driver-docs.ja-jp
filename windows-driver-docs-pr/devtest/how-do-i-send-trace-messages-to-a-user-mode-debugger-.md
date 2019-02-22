---
title: ユーザー モード デバッガーにトレース メッセージを送信する方法
description: ユーザー モード デバッガーにトレース メッセージを送信する方法
ms.assetid: d1a9df10-3339-4518-a42a-abd1123d5e21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2085f7643b12c3315855bcfa481c814b6164f38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532512"
---
# <a name="how-do-i-send-trace-messages-to-a-user-mode-debugger"></a>ユーザー モード デバッガーにトレース メッセージを送信する方法


トレース メッセージをリダイレクトすると、ユーザー モード デバッガーに、追加、WPP\_ソース コードにマクロをデバッグします。 WPP 後、マクロの定義のディレクティブを配置\_コントロール\_GUID 定義します。

WPP\_デバッグ マクロは、トレース メッセージを作成して、マクロで指定される宛先にメッセージをリダイレクトするコードを追加します。 使用することができます、**による DbgPrint**またはこのマクロでヘルパー ルーチン。

ステートメントの形式は次のとおりです。

```
#define WPP_DEBUG(args) printf args , printf("\n");
```

使用することができます**による DbgPrint**または**KdPrint**の代わりに**printf**など。

```
#define WPP_DEBUG(a)   printf a   printf("/n");
```

または

```
#define WPP_DEBUG(b)   DbgPrint("PCI"), DbgPrint b,   DbgPrint("\n");
```

ルーチンを呼び出すステートメントの形式は次のとおりです。

```
WPP_DEBUG((format, ...))
```

ほとんどの形式および引数を使用するには WPP で\_デバッグします。 ただし、% など、トレースに固有の書式の仕様を使用することはできません。IPADDR %。

 

 





