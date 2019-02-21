---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB 基地局情報 OID、モバイル ブロード バンド基地局情報 OID、モバイル ブロード バンドのミニポート ドライバー ベース ステーション情報 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05b14aefae6204f0d24c95fc6f388b70f4451577
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529744"
---
# <a name="oidwwanbasestationsinfo"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO には、サービスを提供し、隣接するセルの既知のモデムに関する情報を取得します。 携帯電話の基地局情報のクエリに関する詳細については、次を参照してください。 [MB ベース ステーションはクエリのサポート](mb-base-stations-information-query-support.md)します。

OID_WWAN_BASE_STATIONS_INFO を使用して、クエリの要求について、 [NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://msdn.microsoft.com/library/windows/hardware/4327021B-93FB-4605-B7D1-A7A6D661C8DF)を格納する構造体、 [WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/66460B28-C2B4-4F05-A133-31A753AF9489)の側面を指定する構造体セルは、応答で送信する近隣セル単位の最大数などです。 モデムのミニポート ドライバーする必要がありますクエリ要求を処理、非同期的に最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知含む、 [NDIS_WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/7C0E0903-F564-4F2B-95F9-FA8512FEF61B)を格納する構造体、 [WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/66460B28-C2B4-4F05-A133-31A753AF9489)提供していると、隣接するベース両方に関する情報を提供する構造体ステーションです。

要求のセットには適用されません。

要請されていないイベントは適用されません。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://msdn.microsoft.com/library/windows/hardware/4327021B-93FB-4605-B7D1-A7A6D661C8DF)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/7C0E0903-F564-4F2B-95F9-FA8512FEF61B)

[WWAN_BASE_STATIONS_INFO](https://msdn.microsoft.com/library/windows/hardware/66460B28-C2B4-4F05-A133-31A753AF9489)

[MB 基地局情報のクエリのサポート](mb-base-stations-information-query-support.md)

