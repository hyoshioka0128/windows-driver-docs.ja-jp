---
title: NVGRE タスク オフロード状態のクエリと変更
description: このセクションでは、NVGRE 対応ミニポートドライバーの汎用ルーティングカプセル化 (NVGRE) タスクオフロード状態を使用して、現在のネットワーク仮想化を照会または変更する方法について説明します。
ms.assetid: 2F493F35-0D6D-4D23-A5CD-FA3990B3EAB5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bee8995ef4bd7e3856efc2ff41103e31d7d79910
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844899"
---
# <a name="querying-and-changing-nvgre-task-offload-state"></a>NVGRE タスク オフロード状態のクエリと変更


このセクションでは、NVGRE 対応ミニポートドライバーの[汎用ルーティングカプセル化 (NVGRE) タスクオフロード状態を使用して、現在のネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)を照会または変更する方法について説明します。 NVGRE タスクオフロードは既定で有効にすることができますが、既定でアクティブにすることはできません。 NIC は、この機能が NDIS プロトコルまたはフィルタードライバーによって明示的に有効化されるまで、カプセル化されたパケットのタスクのオフロードを開始しないようにする必要があります。

## <a name="querying-nvgre-task-offload-state"></a>NVGRE タスクオフロードの状態を照会しています


ミニポートドライバーの現在の NVGRE タスクオフロード状態を照会するために、NDIS プロトコルまたはフィルタードライバーは、現在の\_CONFIG oid 要求の[\_TCP\_オフロード\_の oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)を使用します。 これにより、ndis [ **\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle)構造が返されます。この構造体は、 **EncapsulatedPacketTaskOffloadGre**メンバーが、NDIS を含む[ **\_パケット\_タスク\_オフロード構造\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)されてい **\_の\_オフ**ロードは、GRE でカプセル化されたパケットに対して現在有効になっている場合はサポートされて\_います。それ以外の場合は、 **NDIS\_offload\_** サポートされません。 NDIS はこの OID を処理し、ミニポートには渡しません。

**注  :** ミニポートドライバーで nvgre タスクオフロードがサポートされているかどうかを判断するには、「Nvgre タスクオフロードの決定」の説明に従って、 [\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)の oid 要求を使用してください。 [ネットワークアダプターの機能](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)。

 

## <a name="changing-nvgre-task-offload-state"></a>NVGRE タスクオフロード状態の変更


NDIS プロトコルまたはフィルタードライバーは、 [oid\_TCP\_オフロード\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求を発行して、nvgre タスクオフロードを有効または無効にすることができます。 この OID では、 [**NDIS\_OFFLOAD\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体を使用します。 この構造体では、 **EncapsulatedPacketTaskOffload**メンバーは次の値を持つことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong></p></td>
<td align="left"><p>NVGRE タスクオフロードの状態は変更されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_ON</strong></p></td>
<td align="left"><p>NVGRE タスクオフロードを有効にするには、このフラグを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_OFF</strong></p></td>
<td align="left"><p>NVGRE タスクオフロードを無効にするには、このフラグを指定します。</p></td>
</tr>
</tbody>
</table>

 

ミニポートドライバーは、 [\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求の oid を処理した後で、 [**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態表示を発行する必要があります。を更新し、オフロード状態にします。

ミニポートドライバーが[oid\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求を受信すると、 **NDIS\_オフロード\_SET\_OFF**フラグが指定されている場合、ドライバーは既存のカプセル化を示す必要があります。タスク用に部分的に処理されたパケットは、OID 要求を完了する前にスタックをオフロードします。

標準パケットの基本タスク[オフロードは、oid\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)や\_oid などの既存の oid によって有効になり[\_キュー\_割り当て\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)ます。 **EncapsulatedPacketTaskOffload**メンバー設定は、これらの oid を補完し、カプセル化されたパケットのオフロードも行うように NIC に指示します。

 

 





