---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: ミニポートドライバーは、NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知を使用して、以前の OID_WWAN_NETWORK_BLACKLIST クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_NETWORK_BLACKLIST
ms.localizationpriority: medium
ms.openlocfilehash: b326d8c5e592843399b316b67f6982dc4928c8c7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916655"
---
# <a name="ndis_status_wwan_network_blacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

ミニポートドライバーは、 **NDIS_STATUS_WWAN_NETWORK_BLACKLIST**通知を使用して、以前の[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

ブラックリストの状態のいずれかが感知から not 感知に変化した場合、またはその逆の場合は、一方的なイベントが送信されます。 たとえば、sim が挿入され、プロバイダーが SIM プロバイダーのブラックリストと一致する場合などです。

この通知では、 [**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB ネットワーク ブラックリスト操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)
