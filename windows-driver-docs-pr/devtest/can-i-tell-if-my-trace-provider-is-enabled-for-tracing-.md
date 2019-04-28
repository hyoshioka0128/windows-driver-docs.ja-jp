---
title: トレースのトレース プロバイダーが有効になっているかどうかを知ることができます。
description: トレースのトレース プロバイダーが有効になっているかどうかを知ることができます。
ms.assetid: 8cc4e364-a0bc-4ef3-af3c-c08f3183b548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c101336fe38d88594ef84a79fc61f79730fce9a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375380"
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

 

 





