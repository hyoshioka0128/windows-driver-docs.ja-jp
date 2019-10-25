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




TCP/IP トランスポートによって、NIC が IPsec オフロードバージョン 2 (IPsecOV2) 操作を実行できると判断した後 (「 [nic の Ipsec オフロードバージョン2機能の報告](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)」を参照)、nic のミニポートドライバーによって1つ以上のセキュリティが追加されることを要求します。トランスポートの前に NIC への関連付け (SAs) を使用して、IPsec タスクを NIC にオフロードすることができます。 SAs を追加した後は、TCP/IP トランスポートでそれらを削除または更新することもできます。 IPsecOV2 インターフェイスには、Oid の追加、削除、および更新のための NDIS direct OID インターフェイスが必要です。

**  ndis**は、ndis 6.1 以降のドライバー用の直接 OID 要求インターフェイスを提供します。 [直接 oid 要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は、クエリまたは頻繁に設定される oid 要求をサポートしています。

 

ミニポートドライバーによって1つ以上の SAs が NIC に追加されるように要求するために、TCP/IP トランスポートでは、 [IPSEC\_オフロード\_V2\_\_SA oid を追加する\_、tcp\_タスク\_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)を設定します。 ミニポートドライバーは、 [**IPSEC\_オフロード\_V2 を受信\_\_sa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)構造体を追加し、Sa の IPsecOV2 処理用に NIC を構成します。 正常に OID に設定された\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA を追加すると、ミニポートドライバーによって、IPSEC\_オフロードでオフロード SA を識別するハンドルが初期化され\_V2\_\_SA 構造体を追加します。 トランスポートは、ミニポートドライバーへの後続の要求で、このハンドルを使用します (つまり、送信パスまたは呼び出しで SA を変更または削除します)。 送信パスで SA ハンドルを使用する方法の詳細については、「 [IPsec オフロードバージョン2を使用したネットワークデータの送信](sending-network-data-with-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーは、 [**NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体の**Saoffloadcapacity**メンバーで NIC がサポートできる sa の数を報告します。

ミニポートドライバーでは、受信パケットに対して、 [**NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体の**SaDeleteReq**フラグを設定できます。 TCP/IP トランスポートは、その後、 [IPSEC\_オフロード\_V2 を\_、IPSEC オフロード\_V2\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を1回削除すると、パケットを受信した受信 SA を一度だけ削除し、もう一度\_\_を削除します。削除された受信 SA に対応する送信 SA。

TCP/IP トランスポートは、 [IPSEC\_オフロード\_タスク\_IPSEC オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を削除してパケットを受信した受信 sas を削除し、に対応する送信 sas を削除する\_OID を発行します。受信 SAs が削除されました。 NIC は、対応する OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_SA 要求を削除する前に、これらの SAs を削除することはできません。

TCP/IP トランスポートでは、 [IPSEC\_オフロード\_V2\_更新\_sa oid を\_するために、IPSEC オフロードの\_タスクの oid\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)設定します。シーケンス番号 (ESN)。 ESN をサポートする Nic の場合、ミニポートドライバーがこの要求を受信すると、ドライバーは、 [**IPSEC\_オフロード\_V2\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ipsec_offload_v2_operation)の列挙値に従って、NIC 内の指定された SA のシーケンス番号を更新する必要があります。[**IPSEC\_オフロード\_V2\_\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)構造体の更新の**操作**メンバーで指定されています。

 

 





