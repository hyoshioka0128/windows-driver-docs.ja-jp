---
title: NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_MODEM_LOGGING_CONFIG クエリまたは一連の要求の完了を通知するために、NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 通知を使用します。
ms.assetid: 0370C672-B7A7-4ECE-94F6-FC04407959E4
ms.date: 04/11/2019
keywords: -NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d20ccc643575337460d0fb88ca713be132c8ad47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354172"
---
# <a name="ndisstatuswwanmodemloggingconfig"></a>NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)クエリまたは要求を設定します。

ミニポート ドライバーは、モデムが内部変更について、OS に通知する必要があるシナリオで不要なイベントとしてこの通知を送信します。 現時点では、Windows 10、バージョンが 1903 年でこれらのシナリオは発生しません。

この通知を使用して、 [ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[DSS で MB モデムのログ記録](mb-modem-logging-with-dss.md)

[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
