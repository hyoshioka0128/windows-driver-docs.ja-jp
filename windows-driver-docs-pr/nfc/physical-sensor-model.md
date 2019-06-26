---
title: 物理センサー モデル
description: 物理センサー モデル
ms.assetid: D3887E09-E0A4-4FBC-9D26-344016047235
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11ad14402cee7f7d867c3544df56ff9926d71cd9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386531"
---
# <a name="physical-sensor-model"></a>物理センサー モデル


NFC を実装する 1 つの NFP プロバイダーは、システムで一般的な構成です。 ただしがあります複数 NFP プロバイダー別または同じ NFP テクノロジは、各サポート、特定のシステム。 など特定タブレット フォーム ファクターのシステムは、エッジ、周囲に複数の NFC アンテナを必要があり、タブレットの背面がポイントを使用して追加結合 NFC/TransferJet タッチ - ワイヤレス ドッキング ステーションに接続するために使用します。 この例のシステムで NFP の物理的なモデリングでは、これらの追加のアンテナは 1 つのプロバイダー内で個別にアドレス指定可能ではありません。 システムのメーカーが個別にアドレス可能な配慮を提供するには、アンテナと NFP テクノロジごとに特定 NFP プロバイダーのインスタンスを実装する必要があります。 任意のデバイスは、これらのプロバイダーのいずれかの間で近接になると、公開されたメッセージは、すべてのサブスクライバーに送信されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

