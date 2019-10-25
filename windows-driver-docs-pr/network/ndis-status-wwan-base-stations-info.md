---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
ms.assetid: 57E22B53-5ECC-4B4C-8A98-C1125314868B
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO, ベースステーション情報クエリ状態通知, モバイルブロードバンドベースステーション情報クエリ状態通知, MB ベースステーション情報クエリ状態通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072277dc697616ed62257a0a291e7af5d76a1d3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842104"
---
# <a name="ndis_status_wwan_base_stations_info"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知は、 [OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)クエリ要求への応答として、モデムミニポートドライバーによって送信され、MB ホストにサービスと隣接するベースステーションの両方に関する情報を提供します。

この通知では、 [NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)構造体が使用されます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis. h |

## <a name="see-also"></a>関連項目

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[MB ベースステーション情報クエリ操作](mb-base-stations-information-query-support.md)

