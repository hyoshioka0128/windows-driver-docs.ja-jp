---
title: OID_WWAN_NETWORK_BLACKLIST
description: OID_WWAN_NETWORK_BLACKLIST を取得またはモバイル ブロード バンド (MBB) デバイスのネットワークのブラック リストに関する情報を設定します。
ms.assetid: CD5F0913-73E4-4A04-BB56-76A59D886FF1
ms.date: 08/21/2018
keywords: -OID_WWAN_NETWORK_BLACKLIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9ae817b68faf7a4366dd3c49f97bf88ef21ed171
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539484"
---
# <a name="oidwwannetworkblacklist"></a>OID_WWAN_NETWORK_BLACKLIST

OID_WWAN_NETWORK_BLACKLIST を取得またはモバイル ブロード バンド (MBB) デバイスのネットワークのブラック リストに関する情報を設定します。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)状態の通知含む、 [ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)現在ネットワーク ブラック リストを記述する構造体。

この OID のペイロードを含む、一連の要求について、 [ **NDIS_WWAN_SET_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)モデムが無視される mnc も/MCC 組み合わせの一覧を指定する構造体。

## <a name="remarks"></a>注釈

各クエリまたは一連の要求後に、ミニポート ドライバーを返す必要があります、 [ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)ネットワーク ブラック リストの現在の情報に関する情報を含む構造体。

この OID の使用状況に関する詳細については、[MBIM_CID_MS_NETWORK_BLACKLIST](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations#mbimcidmsnetworkblacklist)を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB のネットワーク ブラック リストの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)

[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)
