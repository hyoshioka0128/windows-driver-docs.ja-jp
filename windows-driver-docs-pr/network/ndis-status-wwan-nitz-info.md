---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_NITZ_INFO 通知を使用して、前の OID_WWAN_NITZ クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 8AC20FB1-FD2E-46B4-97F7-56EC7AA79740
ms.date: 04/11/2019
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_NITZ_INFO
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 28087695fc38d499c3c68468ba726186baf8fb34
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916646"
---
# <a name="ndis_status_wwan_nitz_info"></a>NDIS_STATUS_WWAN_NITZ_INFO

ミニポートドライバーは、 **NDIS_STATUS_WWAN_NITZ_INFO**通知を使用して、前の[OID_WWAN_NITZ](oid-wwan-nitz.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

ミニポートドライバーは、この通知を要請されていないイベントとして送信し、現在のネットワーク時刻とタイムゾーンの intformation を提供します。

この通知では、 [**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[DSS による MB モデムのログ記録](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 
