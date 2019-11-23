---
title: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
description: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
ms.assetid: aaa352c1-fb70-4c96-adda-9710347e2442
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、セキュリティアソシエーション
- セキュリティアソシエーション WDK IPsec オフロード
- SAs WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f269b97f1c82ad011ed87b3177150bfd272de94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844114"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>IPsec Offload Version 2 でのセキュリティ アソシエーションの管理

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




TCP/IP トランスポートは、NIC が IPsec オフロードバージョン 2 (IPsecOV2) 操作を実行できることを判断した後 (「 [nic の Ipsec オフロードバージョン2機能の報告](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)」を参照してください)、トランスポートが nic に対して ipsec タスクの負荷を軽減する前に、nic のミニポートドライバーが nic に1つまたは複数のセキュリティアソシエーション (SAs) を SAs を追加した後は、TCP/IP トランスポートでそれらを削除または更新することもできます。 IPsecOV2 インターフェイスには、Oid の追加、削除、および更新のための NDIS direct OID インターフェイスが必要です。

**  ndis**は、ndis 6.1 以降のドライバー用の直接 OID 要求インターフェイスを提供します。 [直接 oid 要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は、クエリまたは頻繁に設定される oid 要求をサポートしています。

 

ミニポートドライバーによって1つ以上の SAs が NIC に追加されるように要求するために、TCP/IP トランスポートでは、 [IPSEC\_オフロード\_V2\_\_SA oid を追加する\_、tcp\_タスク\_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)を設定します。 ミニポートドライバーは、 [**IPSEC\_オフロード\_V2 を受信\_\_sa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)構造体を追加し、Sa の IPsecOV2 処理用に NIC を構成します。 正常に OID に設定された\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加すると、ミニポートドライバーによって、IPSEC\_オフロード\_V2\_SA 構造を追加するためのオフロード SA を識別するハンドルが初期化されます。\_\_ トランスポートは、ミニポートドライバーへの後続の要求で、このハンドルを使用します (つまり、送信パスまたは呼び出しで SA を変更または削除します)。 送信パスで SA ハンドルを使用する方法の詳細については、「 [IPsec オフロードバージョン2を使用したネットワークデータの送信](sending-network-data-with-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーは、 [**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体の**Saoffloadcapacity**メンバーで NIC がサポートできる sa の数を報告します。

ミニポートドライバーでは、受信パケットに対して、 [**NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体の**SaDeleteReq**フラグを設定できます。 その後、TCP/IP トランスポートは[\_tcp\_タスク\_IPSEC\_オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を一度削除して、パケットが受信した受信 sa を1回削除し、削除された受信 sa に対応する送信 sa を削除します。

TCP/IP トランスポートは、 [IPSEC\_オフロード\_タスク\_IPSEC オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を削除してパケットを受信した受信 sas を削除し、削除された受信 sas に対応する送信 sas を削除するために、OID を発行\_ます。 NIC は、対応する OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA 要求を削除する前に、これらの SAs を削除することはできません。\_

TCP/IP トランスポートは、 [IPSEC\_オフロード\_V2\_更新\_sa oid を\_する oid\_tcp\_タスク](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)を設定します。これにより、ミニポートドライバーは、拡張シーケンス番号 (ESN) を持つ SA の上位ビットを持つ NIC を更新するように要求します。 ESN をサポートする Nic では、ミニポートドライバーがこの要求を受信すると、ドライバーは ipsec [ **\_オフロード\_v2\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ipsec_offload_v2_operation)の列挙値に従って、NIC 内の指定された sa のシーケンス番号を更新する必要があります。これは、 [**IPSEC\_オフロード\_v2\_update\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)構造体の**操作**メンバーで指定されます。

 

 





