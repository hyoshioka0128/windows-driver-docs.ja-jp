---
title: NDIS I/O 作業項目
description: NDIS I/O 作業項目
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- I/o 作業項目 WDK NDIS
- I/o WDK カーネル、NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5da84ccde12642e8eda1a7601b8525c70adf9eb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843547"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 作業項目





ドライバーは、後で実行するために、i/o 作業項目のコールバック関数をキューに含めることができます。 NDIS は、IRQL = パッシブ\_レベルでドライバーが指定したコールバック関数を呼び出します。 これにより、現在の関数から直ちに戻り、ドライバーが低い IRQL で後で動作するようにすることで、システムのパフォーマンスが向上します。

NDIS 6.0 以降では、カーネル i/o 作業項目ルーチン[**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)、および[**ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)のラッパー関数が提供されます。 NDIS では、プライベート[**io\_作業項目**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造ではなく、プライベート**NDIS\_IO\_workitem**構造体を使用します。

NDIS 6.0 ドライバーは、作業項目を割り当てるために[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)関数を呼び出します。 Ndis ミニポートドライバーは、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡すアダプターハンドルを**NdisAllocateIoWorkItem**渡します。 **NdisAllocateIoWorkItem**ハンドルに関連付けられているデバイスオブジェクトを取得し、デバイスオブジェクトを[**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)ルーチンに渡します。 フィルタードライバーはフィルターハンドルを渡します。

**注**  プロトコルドライバーは、プロトコルドライバーとデバイスオブジェクトを関連付けないため、 [**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)を使用できません。

 

NDIS ドライバーは、作業項目をキューにするために[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)関数を呼び出します。 NDIS 作業項目では、 **CriticalWorkQueue**キューの種類を使用します。

NDIS ドライバーは、 [**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)に割り当てられた作業項目に関連付けられているリソースを解放するために、 [**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)関数を呼び出す必要があります。

## <a name="related-topics"></a>関連トピック


[システムワーカースレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)

 

 






