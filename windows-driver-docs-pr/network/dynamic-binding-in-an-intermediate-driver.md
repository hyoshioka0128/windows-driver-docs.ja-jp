---
title: 中間ドライバーの動的バインド
description: 中間ドライバーの動的バインド
ms.assetid: 0b825141-2a19-40c6-82cf-8e897a25b0aa
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK, バインド
- 動的バインド WDK ネットワーク
- バインディング操作の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1948ccc8ebb8013a4e995fe7e21172c0d2fdb5e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386544"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中間ドライバーの動的バインド





中間のドライバーが両方を提供することで基になるミニポート アダプターに動的にバインドをサポートする必要があります、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)と[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数。

NDIS を呼び出すミニポート アダプターが使用可能になるときに、 *ProtocolBindAdapterEx*そのミニポート アダプターにバインドできる任意の中間ドライバーの関数。 バインディング操作の一環として、中間のドライバーがそのミニポート アダプターに関連付けられている仮想ミニポートを初期化する必要があります。 ミニポート アダプターが削除されたとき、NDIS 呼び出し、 *ProtocolUnbindAdapterEx*そのミニポート アダプターにバインドされている中間ドライバーはすべての関数。

次のトピックでは、中間ドライバーでの動的バインド操作に関する追加情報を紹介します。

[バインディング操作を中間ドライバー](intermediate-driver-binding-operations.md)

[中間のドライバーを基になるアダプターを開く](opening-an-adapter-underlying-an-intermediate-driver.md)

[初期化中の仮想ミニポート](initializing-virtual-miniports.md)

[中間のドライバーが操作をバインド解除](intermediate-driver-unbinding-operations.md)

 

 





