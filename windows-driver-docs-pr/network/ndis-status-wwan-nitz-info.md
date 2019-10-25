---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_NITZ_INFO 通知を使用して、以前の OID_WWAN_NITZ クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 8AC20FB1-FD2E-46B4-97F7-56EC7AA79740
ms.date: 04/11/2019
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_NITZ_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cbc69ce1f356ee7220a203a41993169ebcfe0ba1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844666"
---
# <a name="ndis_status_wwan_nitz_info"></a>NDIS_STATUS_WWAN_NITZ_INFO

ミニポートドライバーは、 **NDIS_STATUS_WWAN_NITZ_INFO**通知を使用して、以前の[OID_WWAN_NITZ](oid-wwan-nitz.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

ミニポートドライバーは、この通知を要請されていないイベントとして送信し、現在のネットワーク時刻とタイムゾーンの intformation を提供します。

この通知では、 [**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[DSS でのモデムログ (MB)](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 
