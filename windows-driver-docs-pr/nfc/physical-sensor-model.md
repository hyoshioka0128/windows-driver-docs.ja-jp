---
title: 物理センサー モデル
description: 物理センサー モデル
ms.assetid: D3887E09-E0A4-4FBC-9D26-344016047235
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185493246e401359a7f1cef5e35d6ffe04f07990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539678"
---
# <a name="physical-sensor-model"></a>物理センサー モデル


NFC を実装する 1 つの NFP プロバイダーは、システムで一般的な構成です。 ただしがあります複数 NFP プロバイダー別または同じ NFP テクノロジは、各サポート、特定のシステム。 など特定タブレット フォーム ファクターのシステムは、エッジ、周囲に複数の NFC アンテナを必要があり、タブレットの背面がポイントを使用して追加結合 NFC/TransferJet タッチ - ワイヤレス ドッキング ステーションに接続するために使用します。 この例のシステムで NFP の物理的なモデリングでは、これらの追加のアンテナは 1 つのプロバイダー内で個別にアドレス指定可能ではありません。 システムのメーカーが個別にアドレス可能な配慮を提供するには、アンテナと NFP テクノロジごとに特定 NFP プロバイダーのインスタンスを実装する必要があります。 任意のデバイスは、これらのプロバイダーのいずれかの間で近接になると、公開されたメッセージは、すべてのサブスクライバーに送信されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

