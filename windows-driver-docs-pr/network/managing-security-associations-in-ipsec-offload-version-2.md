---
title: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
description: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
ms.assetid: aaa352c1-fb70-4c96-adda-9710347e2442
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、セキュリティ アソシエーション
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2b3d2d2174209dfa831d475727750743a0d118c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368605"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>IPsec Offload Version 2 でのセキュリティ アソシエーションの管理

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




トランスポートは、NIC が IPsec オフロード バージョン 2 (IPsecOV2) を実行できることを決定後、TCP/IP 操作 (を参照してください[レポート NIC の IPsec オフロード バージョン 2 機能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md))、トランスポート、要求、NIC のミニポート ドライバーを追加します。または、トランスポートは、NIC に IPsec タスク オフロードできます前に NIC に複数のセキュリティ アソシエーション (Sa) SAs を追加した後、TCP/IP トランスポートも削除または更新できます。 IPsecOV2 インターフェイスには、追加、削除、および更新プログラムの Oid の直接の OID の NDIS インターフェイスが必要です。

**注**  NDIS NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 [OID の直接の要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)クエリを実行したり、頻繁に設定されている OID 要求をサポートします。

 

ミニポート ドライバーが、TCP/IP をトランスポート設定の NIC に 1 つ以上の SAs を追加することを要求する、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID。 ミニポート ドライバーが、受信、 [ **IPSEC\_オフロード\_V2\_追加\_SA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_add_sa)構造体し、SA で処理を IPsecOV2 の NIC を構成します。 OID に正常に設定されている\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA、ミニポート ドライバーでオフロード SA を識別するハンドルを初期化します、IPSEC\_オフロード\_V2\_追加\_SA 構造体。 トランスポートは、ミニポート ドライバーに後続の要求でこのハンドルを使用して (つまり、または変更または削除、SA への呼び出しで、送信パス上)。 詳細については、送信パスで SA ハンドルを使用して、次を参照してください。 [IPsec オフロード バージョン 2 でのネットワーク データの送信](sending-network-data-with-ipsec-offload-version-2.md)します。

ミニポート ドライバーは、SAs でサポートできる NIC の数を報告、 **SaOffloadCapacity**のメンバー、 [ **NDIS\_IPSEC\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体。

ミニポート ドライバーを設定できる、 **SaDeleteReq**フラグ、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)受信パケットの構造体。 TCP/IP トランスポートは発行後[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)を削除する 1 つの時間、パケットの受信に使用された着信 SA と 1 回もう一度削除された着信 SA に対応する送信の SA を削除します。

TCP/IP トランスポート問題[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)する受信の SAs を削除する、パケットを受信し、削除された着信 Sa に対応する送信の SAs を削除します。 対応する OID を受信する前に NIC がこれらの SAs を削除する必要があります\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA 要求。

TCP/IP トランスポートの設定、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)を要求する OID ミニポートドライバーは、sa 拡張シーケンス番号 (ESN) を持つより高い順位ビットで NIC を更新します。 ESN、サポートされる nic のドライバーがに従って NIC で指定された SA のシーケンス番号を更新する必要があります、ミニポート ドライバーはこの要求を受け取る、 [ **IPSEC\_オフロード\_V2\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ne-ndis-_ipsec_offload_v2_operation)列挙値で指定されている、**操作**のメンバー、 [ **IPSEC\_オフロード\_V2\_UPDATE\_SA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_update_sa)構造体。

 

 





