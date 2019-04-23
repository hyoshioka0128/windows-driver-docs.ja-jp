---
title: OID_WWAN_MODEM_LOGGING_CONFIG
description: OID_WWAN_MODEM_LOGGING_CONFIG は、モデムされ、どのくらいの頻度が送信されますモデムからホスト経由でデータ サービス Stream (DSS) によって収集されるログの構成に使用されます。
ms.assetid: 418157C2-27B4-4007-9FC4-BEEFEE8EB88B
ms.date: 04/11/2019
keywords:
- OID_WWAN_MODEM_LOGGING_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 57d5cb10e3ac4a8e393b5f69c7caeb308251fb9a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905382"
---
# <a name="oidwwanmodemloggingconfig"></a>OID_WWAN_MODEM_LOGGING_CONFIG

OID_WWAN_MODEM_LOGGING_CONFIG は、モデムされ、どのくらいの頻度が送信されますモデムからホスト経由でデータ サービス Stream (DSS) によって収集されるログの構成に使用されます。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状態通知を含む、 [ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)モデムの現在のログ記録構成を記述する構造体。

セットのペイロードを含む、 [ **NDIS_WWAN_SET_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)モデムのログ記録を構成する方法を指定する構造体。 ミニポート ドライバーする必要がありますセット要求を非同期に処理、最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状態の通知含む、 [ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)モデムのログ記録構成セットの要求の後に記述する構造体。

## <a name="remarks"></a>注釈

ログ セッションを開始する前に、ログ記録を構成する必要があります。 これは、ミニポート ドライバーをサポートするために省略可能な OID です。 ただし、ミニポート ドライバーでは、DSS チャネル経由でモデムのログ記録をサポートする場合は、この OID をサポートしている指定する必要があります。 

この OID の使用状況に関する詳細については、次を参照してください。 [MB モデム DSS をログに記録](mb-modem-logging-with-dss.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[DSS で MB モデムのログ記録](mb-modem-logging-with-dss.md)

[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)

[**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
