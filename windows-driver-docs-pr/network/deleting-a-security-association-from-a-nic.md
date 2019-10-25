---
title: NIC からのセキュリティ アソシエーションの削除
description: NIC からのセキュリティ アソシエーションの削除
ms.assetid: 739a3fef-f0b4-4d7c-9d92-df52fd27915d
keywords:
- セキュリティアソシエーション WDK IPsec オフロード
- SAs WDK IPsec オフロード
- ESP で保護されたパケットの WDK IPsec オフロード、セキュリティアソシエーション
- AH で保護されたパケット WDK IPsec オフロード、セキュリティアソシエーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8316581a4e1bc7295de90b0c5d4b6ba2b3546c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834941"
---
# <a name="deleting-a-security-association-from-a-nic"></a>NIC からのセキュリティ アソシエーションの削除

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




必要に応じて、TCP/IP トランスポートは、IPSEC\_DELETE\_SA を設定して、ポートのセキュリティアソシエーション (SA) を NIC から削除するように要求することができます。この場合は、tcp/ip トランスポートによって[\_tcp\_タスク\_IPSEC を削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)します。

NIC に別の SA 用の領域を作成するために、ミニポートドライバーは、 [**NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)構造体の受信パケットに対して、 **SaDeleteReq**フラグを設定できます。 その後、TCP/IP トランスポートは、IPSEC によって\_IPSEC の\_タスクを\_します。\_\_IPSEC は、パケットを受信した受信セキュリティアソシエーション (SA) を削除し、もう1回、送信 SA を削除します。削除された受信 SA に対応します。 NIC は、対応する OID\_TCP\_タスク\_IPSEC\_DELETE\_SA 要求を受信する前に、これらの SAs のいずれかを削除することはできません。 ミニポートドライバーは、 **Cryptodone**フラグとは無関係に**SaDeleteReq**を設定できます。
