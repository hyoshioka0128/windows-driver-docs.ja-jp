---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB ベースステーション情報 OID、モバイルブロードバンドベースステーション情報 OID、モバイルブロードバンドミニポートドライバーベースステーション情報 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe18d8c132fc4cb13750f12024d58a96c59e4597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843873"
---
# <a name="oid_wwan_base_stations_info"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO は、モデムに認識されているサービスと隣接するセルに関する情報を取得します。 携帯ネットワークベースステーション情報クエリの詳細については、「 [MB ベースステーション情報クエリのサポート](mb-base-stations-information-query-support.md)」を参照してください。

クエリ要求の場合、OID_WWAN_BASE_STATIONS_INFO は[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)構造体を使用します。これには、最大値などのセル情報の側面を指定する[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)構造体が含まれています。応答として送信する近隣セル測定の数。 モデムミニポートドライバーは、クエリ要求を非同期的に処理し、その後、NDIS_ を含む[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知を送信する前に、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻します。 [WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)構造体には、サービスと隣接するベースステーションの両方に関する情報を提供する[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)構造体が含まれています。

Set 要求は適用できません。

要請されていないイベントは適用できません。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)

[MB ベースステーション情報クエリのサポート](mb-base-stations-information-query-support.md)

