---
title: OID_WWAN_MODEM_LOGGING_CONFIG
description: OID_WWAN_MODEM_LOGGING_CONFIG は、モデムによって収集されるログと、データサービスストリーム (DSS) を介してモデムからホストに送信される頻度を構成するために使用されます。
ms.assetid: 418157C2-27B4-4007-9FC4-BEEFEE8EB88B
ms.date: 04/11/2019
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WWAN_MODEM_LOGGING_CONFIG
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9eaaa5fc0776d82c31c3cb5aa5b5f2de00a65ac7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843834"
---
# <a name="oid_wwan_modem_logging_config"></a>OID_WWAN_MODEM_LOGGING_CONFIG

OID_WWAN_MODEM_LOGGING_CONFIG は、モデムによって収集されるログと、データサービスストリーム (DSS) を介してモデムからホストに送信される頻度を構成するために使用されます。

ミニポートドライバーは、クエリ要求を非同期的に処理し、その後、現在のモデムログの構成を記述する[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)構造を含む[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状態通知を送信する前に、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に返す必要があります。

設定ペイロードには、モデムのログの構成方法を指定する[**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)構造が含まれます。 ミニポートドライバーは、セット要求を非同期に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、設定要求後のモデムログの構成を記述する[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)構造を含む[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状態通知を送信する必要があります。

## <a name="remarks"></a>注釈

ログセッションを開始する前にログを構成する必要があります。 これは、サポートするミニポートドライバーの OID です (省略可能)。 ただし、ミニポートドライバーが DSS チャネル経由のモデムのログ記録をサポートしている場合は、この OID をサポートするように指定する必要があります。 

この OID の使用方法の詳細については、「 [DSS を使用した MB モデムのログ](mb-modem-logging-with-dss.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[DSS でのモデムログ (MB)](mb-modem-logging-with-dss.md)

[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)

[**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
