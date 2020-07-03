---
title: NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 通知を使用して、以前の OID_WWAN_MODEM_LOGGING_CONFIG クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 0370C672-B7A7-4ECE-94F6-FC04407959E4
ms.date: 04/11/2019
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6bf26a152b9a71f10bd85bf45aca1a980061d1cc
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917052"
---
# <a name="ndis_status_wwan_modem_logging_config"></a>NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG

ミニポートドライバーは、 **NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG**通知を使用して、以前の[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

ミニポートドライバーは、モデムが内部の変更について OS に通知する必要がある場合に、この通知を要請されていないイベントとして送信します。 現時点では、Windows 10 バージョン1903では、これらのシナリオは発生しません。

この通知では、 [**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[DSS による MB モデムのログ記録](mb-modem-logging-with-dss.md)

[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
