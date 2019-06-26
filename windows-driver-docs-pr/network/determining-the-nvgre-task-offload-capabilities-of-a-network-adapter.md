---
title: ネットワーク アダプターの NVGRE タスク オフロード機能の判断
description: このセクションは、ネットワーク アダプターの NVGRE タスク オフロード機能を決定する方法を説明します
ms.assetid: 1F9C5E7D-5488-47C1-BEDC-D7C640F57511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b63c6222f98f1f1f08d8a8a1bbffb2344c479d4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381396"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>ネットワーク アダプターの NVGRE タスク オフロード機能の判断


サポートしているミニポート ドライバー [Network Virtualization using Generic Routing Encapsulation (NVGRE) タスク オフロード](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)によってこの機能の報告、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体の[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数に渡します[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes).

## <a name="reporting-nvgre-task-offload-capability"></a>レポートの NVGRE タスク オフロード機能


[ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造、**ヘッダー**メンバーを次のように設定する必要があります。

-   **リビジョン**にメンバーを設定する必要があります**NDIS\_オフロード\_リビジョン\_3**します。
-   **サイズ**にメンバーを設定する必要があります**NDIS\_SIZEOF\_NDIS\_オフロード\_リビジョン\_3**します。

NVGRE タスク オフロードのサポートを報告するには、ミニポート ドライバー、次のメンバーを設定、 [ **NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload) 、構造体に格納されている、 **EncapsulatedPacketTaskOffloadGre**のメンバー、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体ミニポート ドライバーの[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数に渡します[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes):

-   設定、 **MaxHeaderSizeSupported**ヘッダーの最大サイズを内部 TCP または UDP ペイロード (TCP または UDP の内部ヘッダーの最後のバイト) これらのタスクのすべての NIC をサポートする必要がありますの先頭に、パケットの先頭からのメンバーオフロードします。 カプセル化の結合がヘッダーがこのサイズを超えるパケットの処理をオフロードできませんプロトコル ドライバーが必要です。

    **注**  256 バイトは、すべての可能なケースが適用される適切な既定値。

     

-   タスクの種類のオフロード、ミニポート ドライバーがカプセル化されたパケットのサポートを示すその他のメンバーを設定します。 これらのメンバーを設定できるフラグの一覧は、の「解説」を参照してください。 [ **NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)します。

## <a name="querying-nvgre-task-offload-capability"></a>NVGRE タスク オフロード機能のクエリを実行します。


ミニポート ドライバーが NVGRE タスク オフロードをサポートしているかどうかを判断するプロトコルとフィルター ドライバーが発行できる、 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID の要求返された、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

**注**  ミニポート ドライバーの NVGRE の機能が現在有効になっているかどうかを調べるには、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 要求」の説明に従って[クエリの実行と変更 NVGRE タスク オフロード状態](querying-and-changing-nvgre-task-offload-state.md)します。

 

**注**  を有効または、ミニポート ドライバーの NVGRE の機能を無効にする、使用、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) 」の説明に従って、OID要求[クエリを実行して、NVGRE タスク オフロードの状態を変更する](querying-and-changing-nvgre-task-offload-state.md)します。

 

 

 





