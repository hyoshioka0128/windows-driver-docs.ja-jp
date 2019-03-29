---
title: トレースのトレース プロバイダーが有効になっているかどうかを知ることができます。
description: トレースのトレース プロバイダーが有効になっているかどうかを知ることができます。
ms.assetid: 8cc4e364-a0bc-4ef3-af3c-c08f3183b548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c101336fe38d88594ef84a79fc61f79730fce9a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582519"
---
# <a name="can-i-tell-if-my-trace-provider-is-enabled-for-tracing"></a>トレースでトレース プロバイダーが有効になっているかどうかわかりますか?


はい、WPP を使用できます\_レベル\_に通知するマクロを有効にするかどうか、[トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションがトレースおよびフラグが有効に有効になっているなど。 これは、場合は、トレース プロバイダーは、ソフトウェア トレースを準備する付加的な処理は特に便利です。

たとえば、フォームの条件を使用できます。

```
If (WPP_LEVEL_ENABLED(flag) {
            // Tracing is enabled
            Prepare to trace
            DoTraceMessage(flag...);
}
```

 

 





