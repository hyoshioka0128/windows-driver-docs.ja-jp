---
title: 中間ドライバーの動的バインド
description: 中間ドライバーの動的バインド
ms.assetid: 0b825141-2a19-40c6-82cf-8e897a25b0aa
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK、バインド
- 動的バインド WDK ネットワーク
- バインド操作 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ecef02738638aa43ca8bc20a759c7471ad52d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838127"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中間ドライバーの動的バインド





中間ドライバーは、 [*protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数と[*protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数の両方を提供することにより、基になるミニポートアダプターへの動的バインドをサポートする必要があります。

ミニポートアダプターが使用可能になると、NDIS は、そのミニポートアダプターにバインドできる任意の中間ドライバーの*Protocolbindadapterex*関数を呼び出します。 バインド操作の一部として、中間ドライバーは、そのミニポートアダプターに関連付けられている仮想ミニポートを初期化する必要があります。 ミニポートアダプターが削除されると、NDIS は、そのミニポートアダプターにバインドされているすべての中間ドライバーの*Protocolunbindadapterex*関数を呼び出します。

次のトピックには、中間ドライバーでの動的バインド操作に関する追加情報が含まれています。

[中間ドライバーバインド操作](intermediate-driver-binding-operations.md)

[中間ドライバーの基になるアダプターを開く](opening-an-adapter-underlying-an-intermediate-driver.md)

[仮想ミニポートの初期化](initializing-virtual-miniports.md)

[中間ドライバーのバインド解除操作](intermediate-driver-unbinding-operations.md)

 

 





