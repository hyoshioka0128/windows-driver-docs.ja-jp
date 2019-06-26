---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB 基地局情報 OID、モバイル ブロード バンド基地局情報 OID、モバイル ブロード バンドのミニポート ドライバー ベース ステーション情報 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6be46c88322efaf928477bf6f94fc97f0f35d84e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362871"
---
# <a name="oidwwanbasestationsinfo"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO には、サービスを提供し、隣接するセルの既知のモデムに関する情報を取得します。 携帯電話の基地局情報のクエリに関する詳細については、次を参照してください。 [MB ベース ステーションはクエリのサポート](mb-base-stations-information-query-support.md)します。

OID_WWAN_BASE_STATIONS_INFO を使用して、クエリの要求について、 [NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)を格納する構造体、 [WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)の側面を指定する構造体セルは、応答で送信する近隣セル単位の最大数などです。 モデムのミニポート ドライバーする必要がありますクエリ要求を処理、非同期的に最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知含む、 [NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)を格納する構造体、 [WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)提供していると、隣接するベース両方に関する情報を提供する構造体ステーションです。

要求のセットには適用されません。

要請されていないイベントは適用されません。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)

[MB 基地局情報のクエリのサポート](mb-base-stations-information-query-support.md)

