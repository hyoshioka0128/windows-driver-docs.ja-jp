---
title: NDIS ポートの解放
description: NDIS ポートの解放
ms.assetid: ae7b608d-6105-4fdc-b805-0f0101d7c218
keywords:
- ポート WDK NDIS、解放
- NDIS ポート WDK、解放
- NDIS ポートの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 593c737f5512216416ee25f8e61209a7fb1c59d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842124"
---
# <a name="freeing-an-ndis-port"></a>NDIS ポートの解放





ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数のミニポートアダプターに[割り当て](allocating-an-ndis-port.md)られているすべての NDIS ポートを解放する必要があります。 次に示す2つのケースを除き、 [**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)を呼び出すことで、いつでもポートを解放できます。

これらの場合、ミニポートドライバーは、割り当てられているすべてのポートを解放する必要があります。

-   ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が失敗した場合は、割り当てられているすべてのポートを解放する必要があります。
-   ミニポートアダプターが停止している場合は、ドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数で、割り当てられているすべてのポートを解放する必要があります。

このような場合、ミニポートドライバーは単に[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)を呼び出すことはできません。

-   ポートが既定のポートの場合は、NDIS によって自動的に解放されるので、ミニポートドライバーはそれを解放できません。 [既定のポート](default-ndis-port.md)を解放しようとすると、 [**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)は NDIS\_の状態\_無効な\_ポートエラーを返します。
-   ポートがアクティブである場合、ミニポートドライバーは、 [**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)を呼び出す前に非アクティブ化する必要があります。

## <a name="related-topics"></a>関連トピック


[NDIS ポートを割り当てています](allocating-an-ndis-port.md)

[NDIS ポートの非アクティブ化](deactivating-an-ndis-port.md)

[既定の NDIS ポート](default-ndis-port.md)

 

 






