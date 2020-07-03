---
title: OID_WWAN_NETWORK_BLACKLIST
description: OID_WWAN_NETWORK_BLACKLIST モバイルブロードバンド (MBB) デバイスのネットワークブラックリストに関する情報を取得または設定します。
ms.assetid: CD5F0913-73E4-4A04-BB56-76A59D886FF1
ms.date: 08/21/2018
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_NETWORK_BLACKLIST
ms.localizationpriority: medium
ms.openlocfilehash: 48948ab939ec6c18e26eea4035f4e1224454290f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916875"
---
# <a name="oid_wwan_network_blacklist"></a>OID_WWAN_NETWORK_BLACKLIST

OID_WWAN_NETWORK_BLACKLIST モバイルブロードバンド (MBB) デバイスのネットワークブラックリストに関する情報を取得または設定します。

ミニポートドライバーは、クエリ要求を非同期に処理し、その後、現在のネットワークブラックリストを記述する[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)構造を含む[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)状態通知を送信する前に、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返す必要があります。

セット要求の場合、この OID のペイロードには、モデムによって無視される MNC/MCC の組み合わせの一覧を指定する[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)構造が含まれています。

## <a name="remarks"></a>注釈

各クエリまたは設定要求の後に、ミニポートドライバーは、現在のネットワークブラックリスト情報に関する情報を含む[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)構造体を返す必要があります。

この OID の使用方法の詳細については、「 [MBIM_CID_MS_NETWORK_BLACKLIST](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations#mbimcidmsnetworkblacklist)」を参照してください。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB ネットワーク ブラックリスト操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)

[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)
