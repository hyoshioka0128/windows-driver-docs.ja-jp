---
title: NVGRE タスク オフロード状態のクエリと変更
description: このセクションでは、クエリまたは NVGRE 対応のミニポート ドライバーの状態の Generic Routing Encapsulation (NVGRE) タスク オフロードを使用して現在のネットワーク仮想化を変更する方法について説明します。
ms.assetid: 2F493F35-0D6D-4D23-A5CD-FA3990B3EAB5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e15256c729f6a05bae56d6e1f0ada41ac60b5a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385437"
---
# <a name="querying-and-changing-nvgre-task-offload-state"></a>NVGRE タスク オフロード状態のクエリと変更


このセクションは、クエリまたは現在を変更する方法を説明します[Network Virtualization using Generic Routing Encapsulation (NVGRE) タスク オフロード](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)NVGRE 対応のミニポート ドライバーの状態。 既定では、NVGRE タスク オフロードを有効にすることができますが、運用上、既定でアクティブにする必要がありますできません。 NIC では、NDIS プロトコルまたはフィルター ドライバーによってこの機能を明示的に有効になるまでにカプセル化されたパケットをタスク オフロードを実行することは開始する必要があります。

## <a name="querying-nvgre-task-offload-state"></a>NVGRE タスク オフロードの状態のクエリを実行します。


ミニポート ドライバーの現在の NVGRE タスク オフロード状態を照会する NDIS プロトコルまたはフィルター ドライバーを使用して、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 要求。 これにより返されます、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_offload_handle)持つ**EncapsulatedPacketTaskOffloadGre**メンバーは、 [ **NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)を含む構造体**NDIS\_オフロード\_サポートされています。** GRE カプセル化パケットをそれらのオフロードが現在有効になっている場合と**NDIS\_オフロード\_いない\_サポートされている**それ以外の場合。 NDIS は、この OID を処理し、ミニポートに渡しません。

**注**  ミニポート ドライバーが NVGRE タスク オフロードをサポートしているかどうかを調べるには、 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID説明している要求[ネットワーク アダプターの NVGRE タスク オフロード機能を判断する](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)します。

 

## <a name="changing-nvgre-task-offload-state"></a>NVGRE タスク オフロードの状態を変更します。


NDIS プロトコルまたはフィルター ドライバーが有効にまたは発行することにより、NVGRE タスク オフロードを無効にする、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) OID 要求。 この OID を使用して、 [ **NDIS\_オフロード\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体。 この構造で、 **EncapsulatedPacketTaskOffload**メンバーは、次の値を持つことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong></p></td>
<td align="left"><p>NVGRE タスク オフロードの状態は変更されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_ON</strong></p></td>
<td align="left"><p>NVGRE タスク オフロードを有効にするには、このフラグを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_OFF</strong></p></td>
<td align="left"><p>NVGRE タスク オフロードを無効にするには、このフラグを指定します。</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーのプロセスの後、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) OID 要求と、それを発行する必要があります、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)で更新された状態の表示状態の負荷を軽減します。

ミニポート ドライバーが受信すると、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) OID 要求を**NDIS\_オフロード\_設定\_オフ**フラグを指定すると、既存のすべてのタスクは、スタックに OID 要求を完了する前に、オフロードの部分的に処理されたパケットをカプセル化されたドライバーを示す必要があります。

基本タスクのオフロードなど標準のパケットを既存の Oid を有効にするの[OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)と[OID\_受信\_フィルター\_割り当てる\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)します。 **EncapsulatedPacketTaskOffload**メンバーの設定は、これらの Oid を補足するものし、NIC もカプセル化されたパケットのこれらのオフロードを実行するように指示します。

 

 





