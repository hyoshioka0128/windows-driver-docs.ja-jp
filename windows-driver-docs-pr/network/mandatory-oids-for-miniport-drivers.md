---
title: ミニポート ドライバーの必須 OID
description: このトピックでは、ミニポート ドライバーに必須の Oid をについて説明します
ms.assetid: e4a620b4-de8f-4c1a-be94-b0ec97fa9791
keywords:
- ミニポート ドライバー、ネットワークの必須の NDIS Oid、必須の Oid WDK では、必須の Oid の必須の Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a236c5de40c56374108cbbd45d89c22c089558c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578162"
---
# <a name="mandatory-oids-for-miniport-drivers"></a>ミニポート ドライバーの必須 OID

次の表には、必須のすべてのミニポート ドライバーの Oid が一覧表示します。 ミニポート ドライバーは、NDIS バージョンとなどがサポートするサービスに応じて、追加の Oid をサポートする必要があります。

- 接続指向オブジェクト 
- いる CoNDIS  
- イーサネット統計情報 OID 
- ヘッダー データの分割の Oid 
- Hyper-V 拡張可能スイッチ OID 
- IPsec オフロード バージョン 2 の Oid 
- MB の Oid 
- ネイティブの 802.11 ワイヤレス LAN Oid 
- NDIS TCP/IP オフロード Oid 
- NDKPI Oid 
- 運用上の電源管理の Oid 
- 受信フィルター Oid の概要 
- フィルターの Oid が表示されます。 
- Receive Side Scaling の Oid 
- リモート NDIS OID 
- 電源管理用の必須およびオプションの OID 
- SR-IOV OID 
- 統計の電源管理の Oid 
- タスクのオフロード オブジェクト 
- VMQ Oid

テーブルの"O/M"の列。 

- "M"は「必須」を意味し、"O"を"optional"の意味
- "N/A"の「O/M クエリ」列は、OID が要求を設定するため、ミニポート ドライバーがのみをサポートする必要がある、NDIS OID クエリ要求を処理し、ミニポート ドライバーには送信しませんを意味します。 
- 「O/M クエリ」列にエントリがない場合は、設定専用の OID が、この OID。
- 「O/M の設定」列にエントリがない場合は、クエリ専用の OID が、この OID。

| OID | クエリの O/分 | セットの O/分 | コメント |
| --- | --- | --- | --- |
| [OID_GEN_CURRENT_LOOKAHEAD](oid-gen-current-lookahead.md) | N/A | M | NDIS は、クエリとミニポート ドライバーの失敗したセット要求を処理します。 NDIS は、ミニポート ドライバーに有効な一連の要求を送信します。 同じ情報を取得できます[OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md)します。 |
| [OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md) | N/A | M | クエリは必須ではありません。 セットは必須です。 |
| [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) | M | M |   |
| [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) |   | M |   |
| [OID_GEN_MAXIMUM_TOTAL_SIZE](oid-gen-maximum-total-size.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_RCV_OK](oid-gen-rcv-ok.md) | M |   | NDIS ミニポート ドライバーには、この OID を処理せず[OID_GEN_STATISTICS](oid-gen-statistics.md)この情報は含まれません。 **注意**:NDIS は、それを処理しない限り、統計の Oid は必須です。 |
| [OID_GEN_RECEIVE_BLOCK_SIZE](oid-gen-receive-block-size.md) | M |   | NDIS は、ミニポート ドライバーには、この OID を処理しません。 |
| [OID_GEN_RECEIVE_BUFFER_SPACE](oid-gen-receive-buffer-space.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_STATISTICS](oid-gen-statistics.md) | M |   |   |
| [OID_GEN_TRANSMIT_BLOCK_SIZE](oid-gen-transmit-block-size.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_TRANSMIT_BUFFER_SPACE](oid-gen-transmit-buffer-space.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_VENDOR_DESCRIPTION](oid-gen-vendor-description.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_VENDOR_DRIVER_VERSION](oid-gen-vendor-driver-version.md) | M |   | この情報を取得するには、その他の方法はありません。 |
| [OID_GEN_VENDOR_ID](oid-gen-vendor-id.md) | M |   | この情報を取得するには、その他の方法はありません。 独立系ハードウェア ベンダーのフィルター ドライバーまたは中間ドライバーは、この OID をクエリがあります。 |
| [OID_GEN_XMIT_OK](oid-gen-xmit-ok.md) | M |   | NDIS はこの OID を処理しないと[OID_GEN_STATISTICS](oid-gen-statistics.md)この情報は含まれません。 **注意**:NDIS は、それを処理しない限り、統計の Oid は必須です。 |

