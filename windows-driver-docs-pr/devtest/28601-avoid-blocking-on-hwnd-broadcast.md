---
title: C28601
description: 警告 C28601 では、HWND_BROADCAST でブロックされないようにします。
ms.assetid: 51fc27da-012a-4cf3-adbf-bd7f7c497b01
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28601
ms.openlocfilehash: 4d315286d239433a5e6a33e242fa315a819a3418
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579620"
---
# <a name="c28601"></a>C28601


C28601 を警告します。HWND でブロックされないように\_ブロードキャスト

この警告は、アプリケーションと呼ばれることを示します**SendMessage**で、 **HWND\_ブロードキャスト**フラグ、このメッセージがブロードキャストの応答すべての windows まで、スレッドをブロックします. ただし、応答していない別のウィンドウがある場合、現在のスレッドもブロックされます。

この問題を解決するには使用**PostMessage**代わりに、そのためれていたブロック呼び出しです。 またの使用を回避する**HWND\_ブロードキャスト**特定のウィンドウにメッセージを送信します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の呼び出しには、プロセスが応答を停止する可能性があります。

```
SendMessage(HWND_BROADCAST, ... );
```

 

 





