---
title: ドライバー インターフェイス
description: ドライバー インターフェイス
ms.assetid: cb5e06c3-6add-4eba-b794-861d567a3047
keywords:
- 強制的にフィードバック ドライバー WDK を非表示にサポートされるメソッド
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c2eda901ce83fdfdfa282f9d9f305592142ce323
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375741"
---
# <a name="driver-interface"></a>ドライバー インターフェイス





フォース フィードバック ドライバーでは、COM ベースで、ドライバーのインスタンスは DirectInput によって作成されます。 インターフェイスが指定されている場合が"VJoyD"VJoyD ミニドライバーは VJoyD によって読み込まれます。 両方のドライバー パスは、エクスポートした次のメソッドをサポートします。

[*DestroyEffect*](https://docs.microsoft.com/previous-versions/ff538410(v=vs.85))

[*初期化します。* ](https://docs.microsoft.com/previous-versions/ff541025(v=vs.85))

[*DownloadEffect*](https://docs.microsoft.com/previous-versions/ff538601(v=vs.85))

[*GetEffectStatus*](https://docs.microsoft.com/previous-versions/ff538772(v=vs.85))

[*GetForceFeedbackState*](https://docs.microsoft.com/previous-versions/ff538776(v=vs.85))

[*エスケープ*](https://docs.microsoft.com/previous-versions/ff538680(v=vs.85))

[*SendForceFeedbackCommand*](https://docs.microsoft.com/previous-versions/ff543387(v=vs.85))

[*SetGain*](https://docs.microsoft.com/previous-versions/ff543406(v=vs.85))

[*StartEffect*](https://docs.microsoft.com/previous-versions/ff543458(v=vs.85))

[*StopEffect*](https://docs.microsoft.com/previous-versions/ff543460(v=vs.85))

この機能はすべてフォース フィードバック デバイスをサポートします。

 

 




