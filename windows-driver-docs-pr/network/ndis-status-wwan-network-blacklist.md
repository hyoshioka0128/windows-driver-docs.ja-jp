---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: ミニポートドライバーは、NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知を使用して、以前の OID_WWAN_NETWORK_BLACKLIST クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_NETWORK_BLACKLIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 4a64bc693e49fdd6b09906464eed187e45fa2bcd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844668"
---
# <a name="ndis_status_wwan_network_blacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

ミニポートドライバーは、 **NDIS_STATUS_WWAN_NETWORK_BLACKLIST**通知を使用して、以前の[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

ブラックリストの状態のいずれかが感知から not 感知に変化した場合、またはその逆の場合は、一方的なイベントが送信されます。 たとえば、sim が挿入され、プロバイダーが SIM プロバイダーのブラックリストと一致する場合などです。

この通知では、 [**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB ネットワークブラックリスト操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)
