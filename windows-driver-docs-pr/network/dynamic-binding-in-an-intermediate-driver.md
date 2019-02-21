---
title: 中間のドライバーでの動的バインド
description: 中間のドライバーでの動的バインド
ms.assetid: 0b825141-2a19-40c6-82cf-8e897a25b0aa
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK, バインド
- 動的バインド WDK ネットワーク
- バインディング操作の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7d6ac50dfa604f9ffe8392ac291a3c60239602
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559356"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中間のドライバーでの動的バインド





中間のドライバーが両方を提供することで基になるミニポート アダプターに動的にバインドをサポートする必要があります、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)と[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。

NDIS を呼び出すミニポート アダプターが使用可能になるときに、 *ProtocolBindAdapterEx*そのミニポート アダプターにバインドできる任意の中間ドライバーの関数。 バインディング操作の一環として、中間のドライバーがそのミニポート アダプターに関連付けられている仮想ミニポートを初期化する必要があります。 ミニポート アダプターが削除されたとき、NDIS 呼び出し、 *ProtocolUnbindAdapterEx*そのミニポート アダプターにバインドされている中間ドライバーはすべての関数。

次のトピックでは、中間ドライバーでの動的バインド操作に関する追加情報を紹介します。

[バインディング操作を中間ドライバー](intermediate-driver-binding-operations.md)

[中間のドライバーを基になるアダプターを開く](opening-an-adapter-underlying-an-intermediate-driver.md)

[初期化中の仮想ミニポート](initializing-virtual-miniports.md)

[中間のドライバーが操作をバインド解除](intermediate-driver-unbinding-operations.md)

 

 





