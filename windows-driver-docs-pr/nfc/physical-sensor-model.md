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
ms.openlocfilehash: c9808776e342698949d587a4093c4f62f451bbb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831547"
---
# <a name="physical-sensor-model"></a>物理センサー モデル


システムでの一般的な構成では、NFC を実装する NFP プロバイダーが1つ必要です。 ただし、特定のシステムに複数の NFP プロバイダーが存在し、それぞれが異なるまたは同じ NFP テクノロジをサポートしている場合があります。 たとえば、特定のタブレットフォームファクターシステムでは、エッジ周辺に複数の NFC アンテナが配置されている場合があります。また、タブレットの背面には、ワイヤレスドックへの接続に使用される追加の追加の NFC/TransferJet タッチポイントが必要になる場合があります。 この例のシステムでは、NFP の物理的なモデリングで、このような追加のアンテナを1つのプロバイダー内で個別にアドレス指定することはできません。 個別にアドレス指定可能な個々を提供するには、システムメーカーは、アンテナおよび NFP テクノロジごとに特定の NFP プロバイダーインスタンスを実装する必要があります。 これらのプロバイダーのいずれかでデバイスが近接されると、公開されたメッセージはすべてのサブスクライバーに送信されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

