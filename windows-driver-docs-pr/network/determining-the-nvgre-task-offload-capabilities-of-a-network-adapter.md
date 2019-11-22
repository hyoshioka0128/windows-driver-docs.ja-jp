---
title: ネットワーク アダプターの NVGRE タスク オフロード機能の判断
description: このセクションでは、ネットワークアダプターの NVGRE タスクオフロード機能を確認する方法について説明します。
ms.assetid: 1F9C5E7D-5488-47C1-BEDC-D7C640F57511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73c3c66ed85679352edcf0c64ea747ddae6502c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834899"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>ネットワーク アダプターの NVGRE タスク オフロード機能の判断


[汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)をサポートするミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を使用する[**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造を使用してこの機能を報告します。[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡します。

## <a name="reporting-nvgre-task-offload-capability"></a>NVGRE タスクオフロード機能のレポート


[**NDIS\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体では、次のように**ヘッダー**メンバーを設定する必要があります。

-   **リビジョン**メンバーを**NDIS\_OFFLOAD\_revision\_3**に設定する必要があります。
-   **Size**メンバーは、 **ndis\_SIZEOF\_ndis\_OFFLOAD\_REVISION\_3**に設定する必要があります。

NVGRE タスクオフロードのサポートを報告するために、ミニポートドライバーは、 [ **\_パケット\_タスク\_\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)されている次のメンバーを、ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が[**NDISMSETMINIPORTATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡す[**ndis\_offload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体の**EncapsulatedPacketTaskOffloadGre**メンバーに格納されています。

-   **MaxHeaderSizeSupported**メンバーを、パケットの先頭から内部 TCP または udp ペイロードの先頭までの最大ヘッダーサイズ (tcp または udp 内部ヘッダーの最後のバイト) に設定します。これにより、NIC は、これらすべてのタスクオフロードに対してサポートする必要があります。 プロトコルドライバーは、結合されたカプセル化ヘッダーがこのサイズを超えているパケットの処理をオフロードすることは想定されていません。

    **注**  256 バイトは、可能なすべてのケースに対応するための適切な既定値です。

     

-   他のメンバーを設定して、カプセル化されたパケットに対してミニポートドライバーがサポートするタスクオフロードの種類を指定します。 これらのメンバーに対して設定できるフラグの一覧については、「 [**NDIS\_カプセル化された\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)」の「解説」を参照してください。

## <a name="querying-nvgre-task-offload-capability"></a>NVGRE タスクオフロード機能のクエリを実行しています


ミニポートドライバーが NVGRE タスクオフロードをサポートしているかどうかを判断するために、プロトコルとフィルタードライバーは、 [**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造を返す[oid\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)の oid 要求を発行できます。

**注  :** ポートドライバーの nvgre 機能が現在有効になっているかどうかを判断するには、「Nvgre タスクのクエリと変更」の説明に従って、[現在\_構成 Oid 要求の oid\_TCP\_オフロード\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)を使用します。 [オフロードの状態](querying-and-changing-nvgre-task-offload-state.md)。

 

**注:** ミニポートドライバーの nvgre 機能を有効または無効にするには  「 [Nvgre タスクオフロード状態のクエリと変更](querying-and-changing-nvgre-task-offload-state.md)」の説明に従って、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)の oid 要求を使用します。

 

 

 





