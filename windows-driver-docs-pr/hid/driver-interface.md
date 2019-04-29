---
title: ドライバー インターフェイス
description: ドライバー インターフェイス
ms.assetid: cb5e06c3-6add-4eba-b794-861d567a3047
keywords:
- 強制的にフィードバック ドライバー WDK を非表示にサポートされるメソッド
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e13c09772a151d3f0b04d670b10382e573acbfd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388955"
---
# <a name="driver-interface"></a>ドライバー インターフェイス





フォース フィードバック ドライバーでは、COM ベースで、ドライバーのインスタンスは DirectInput によって作成されます。 インターフェイスが指定されている場合が"VJoyD"VJoyD ミニドライバーは VJoyD によって読み込まれます。 両方のドライバー パスは、エクスポートした次のメソッドをサポートします。

[*DestroyEffect*](https://msdn.microsoft.com/library/windows/hardware/ff538410)

[*初期化します。*](https://msdn.microsoft.com/library/windows/hardware/ff541025)

[*DownloadEffect*](https://msdn.microsoft.com/library/windows/hardware/ff538601)

[*GetEffectStatus*](https://msdn.microsoft.com/library/windows/hardware/ff538772)

[*GetForceFeedbackState*](https://msdn.microsoft.com/library/windows/hardware/ff538776)

[*エスケープ*](https://msdn.microsoft.com/library/windows/hardware/ff538680)

[*SendForceFeedbackCommand*](https://msdn.microsoft.com/library/windows/hardware/ff543387)

[*SetGain*](https://msdn.microsoft.com/library/windows/hardware/ff543406)

[*StartEffect*](https://msdn.microsoft.com/library/windows/hardware/ff543458)

[*StopEffect*](https://msdn.microsoft.com/library/windows/hardware/ff543460)

この機能はすべてフォース フィードバック デバイスをサポートします。

 

 




