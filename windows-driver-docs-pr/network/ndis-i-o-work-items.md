---
title: NDIS I/O 作業項目
description: NDIS I/O 作業項目
ms.assetid: 4f966ff3-2092-495f-863f-50f079085fa6
keywords:
- 作業項目の I/O WDK NDIS
- I/O WDK カーネル、NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f66c817bde997454caf5fb1f07202c5f95afe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385515"
---
# <a name="ndis-io-work-items"></a>NDIS I/O 作業項目





ドライバー キューに I/O の作業項目コールバック関数は、後で実行できます。 NDIS は IRQL でドライバーが指定したコールバック関数を呼び出す = パッシブ\_レベル。 これにより、すぐに返される現在の関数と低い IRQL で後で作業を実行するドライバーを許可することでシステムのパフォーマンスが向上します。

NDIS 6.0 以降では、ラッパー関数カーネル I/O 作業項目のルーチン[ **IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)、 [ **IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)、[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)します。 プライベートではなく[ **IO\_作業項目**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造、NDIS は、プライベート**NDIS\_IO\_WORKITEM**構造体。

NDIS 6.0 のドライバーの呼び出し、 [ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)を作業項目を割り当てる関数。 NDIS ミニポート ドライバーを渡す**NdisAllocateIoWorkItem**アダプターの処理に渡されるその NDIS、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 **NdisAllocateIoWorkItem** 、ハンドルに関連付けられたデバイス オブジェクトを取得し、デバイスにオブジェクトを渡します、 [ **IoAllocateWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)ルーチン。 フィルター ドライバー フィルター ハンドルを渡します。

**注**  プロトコル ドライバーを使用できない[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem) NDIS は、デバイス オブジェクトをプロトコル ドライバーを関連付けないので。

 

NDIS ドライバー呼び出し、 [ **NdisQueueIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisqueueioworkitem)関数作業項目をキューに登録します。 NDIS 作業項目の使用、 **CriticalWorkQueue**キューの種類。

NDIS ドライバーを呼び出す必要があります、 [ **NdisFreeIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreeioworkitem)いる職場に関連付けられているリソースを解放関数項目[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)割り当てられます。

## <a name="related-topics"></a>関連トピック


[システムのワーカー スレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)

 

 






