---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
ms.assetid: 57E22B53-5ECC-4B4C-8A98-C1125314868B
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO, ベースステーション情報クエリの状態通知, モバイルブロードバンドベースステーション情報クエリ状態通知, MB ベースステーション情報クエリ状態通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47302a63b362d62ef4fb0536613c3203f14f0aa0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916548"
---
# <a name="ndis_status_wwan_base_stations_info"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知は、 [OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)クエリ要求に応答して、モデムミニポートドライバーによって送信され、MB ホストにサービスと隣接するベースステーションの両方に関する情報を提供します。

この通知では、 [NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1709**ヘッダー**: Ndis. h

## <a name="see-also"></a>こちらもご覧ください

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[MB ベースステーション情報クエリ操作](mb-base-stations-information-query-support.md)

