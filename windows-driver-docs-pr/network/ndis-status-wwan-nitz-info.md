---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_NITZ クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_NITZ_INFO 通知を使用します。
ms.assetid: 8AC20FB1-FD2E-46B4-97F7-56EC7AA79740
ms.date: 04/11/2019
keywords: -NDIS_STATUS_WWAN_NITZ_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 57b7e0c8bb8841e0ac9b889f223c3c2bc6020dbb
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905441"
---
# <a name="ndisstatuswwannitzinfo"></a>NDIS_STATUS_WWAN_NITZ_INFO

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_NITZ_INFO**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_NITZ](oid-wwan-nitz.md)クエリ要求。

ミニポート ドライバーでは、現在のネットワーク時刻とタイム ゾーンの intformation を提供する要請されていないイベントとしてこの通知を送信します。

この通知を使用して、 [ **NDIS_WWAN_NITZ_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[DSS で MB モデムのログ記録](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 
