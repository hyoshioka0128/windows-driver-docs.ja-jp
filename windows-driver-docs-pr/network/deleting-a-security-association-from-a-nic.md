---
title: NIC からのセキュリティ アソシエーションの削除
description: NIC からのセキュリティ アソシエーションの削除
ms.assetid: 739a3fef-f0b4-4d7c-9d92-df52fd27915d
keywords:
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
- WDK の IPsec ESP により保護されたパケットのオフロード、セキュリティ アソシエーション
- AH で保護されたパケット WDK IPsec オフロード、セキュリティ アソシエーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c07e4765913047acd5a10d654cc09480f5e2d581
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379220"
---
# <a name="deleting-a-security-association-from-a-nic"></a>NIC からのセキュリティ アソシエーションの削除

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




必要に応じて、TCP/IP トランスポート設定できます[OID\_TCP\_タスク\_IPSEC\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)ミニポート ドライバーが、セキュリティ アソシエーション (SA) を削除することを要求するにはNIC から

NIC で SA をもう 1 つのスペースを作成するミニポート ドライバーを設定できます、 **SaDeleteReq**フラグ、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)受信パケットの構造体。 TCP/IP トランスポートは、OID を後で発行\_TCP\_タスク\_IPSEC\_削除\_SA にパケットが受信された受信セキュリティ アソシエーション (SA) を削除する 1 つの時間と別の日時に削除された着信 SA に対応する送信の SA を削除します。 NIC を削除しないでこれらの SAs のいずれかの対応する OID を受信する前に\_TCP\_タスク\_IPSEC\_削除\_SA 要求。 ミニポート ドライバーを設定できます**SaDeleteReq**とは無関係に、 **CryptoDone**フラグ。
