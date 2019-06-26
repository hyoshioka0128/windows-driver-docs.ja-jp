---
title: NDIS ポートの解放
description: NDIS ポートの解放
ms.assetid: ae7b608d-6105-4fdc-b805-0f0101d7c218
keywords:
- ポートの解放の WDK NDIS
- NDIS、WDK のポートの解放
- NDIS ポートの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24b13066dc5617ddb86fa1ef2240f613f4dad4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382763"
---
# <a name="freeing-an-ndis-port"></a>NDIS ポートの解放





ミニポート ドライバーをすべて解放する必要があります NDIS ポートを[割り当てます](allocating-an-ndis-port.md)ミニポート アダプターでその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 できる無料ポートをいつでも呼び出すことによって[ **NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)、次に示す 2 つの場合を除いて。

ミニポート ドライバーでは、このような場合に割り当てられているすべてのポートを解放する必要があります。

-   場合、ドライバーの[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数が失敗にする必要があります無料すべて割り当てられたポート。
-   ミニポート アダプターを停止にしたかどうか、ドライバーの[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数が割り当てられているすべてのポートを解放する必要があります。

ミニポート ドライバーは単に呼び出すことはできません[ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)このような場合。

-   ポートが既定のポートの場合は、NDIS 解放され、自動的に、ように、ミニポート ドライバーは解放する必要があります。 解放しようとすると、[既定のポート](default-ndis-port.md)、 [ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport) 、NDIS を返します\_状態\_無効な\_ポート エラー。
-   ポートがアクティブな場合、ミニポート ドライバーが呼び出す前にアクティブ化する必要があります[ **NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)します。

## <a name="related-topics"></a>関連トピック


[NDIS ポートの割り当てください。](allocating-an-ndis-port.md)

[NDIS ポートを非アクティブ化](deactivating-an-ndis-port.md)

[NDIS の既定のポート](default-ndis-port.md)

 

 






