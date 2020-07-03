---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB ベースステーション情報 OID、モバイルブロードバンドベースステーション情報 OID、モバイルブロードバンドミニポートドライバーベースステーション情報 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a1c5cbca3987d9f5c3ac678b8e3d233f51f85c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916371"
---
# <a name="oid_wwan_base_stations_info"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO は、モデムに認識されているサービスと隣接するセルに関する情報を取得します。 携帯ネットワークベースステーション情報クエリの詳細については、「 [MB ベースステーション情報クエリのサポート](mb-base-stations-information-query-support.md)」を参照してください。

クエリ要求の場合、OID_WWAN_BASE_STATIONS_INFO は[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)構造を使用します。これには、応答として送信する近隣セル測定の最大数など、セル情報の側面を指定する[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)構造が含まれます。 モデムミニポートドライバーは、クエリ要求を非同期的に処理し、最初に[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)構造を含む[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知を送信する前に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返す必要があります。その後、サービス側と隣接するベースステーションの両方に関する情報を提供する[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)構造が含まれます。

Set 要求は適用できません。

要請されていないイベントは適用できません。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1709**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)

[MB ベース ステーション情報クエリのサポート](mb-base-stations-information-query-support.md)

