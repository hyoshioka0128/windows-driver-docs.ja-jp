---
title: OID_WWAN_PCO
description: OID_WWAN_PCO は、オペレータネットワークからモデムが受信した PCO 値の状態とペイロードを報告します。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO、PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 848ade6606bcba8bf914d65bb4faa3491a622ddb
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918134"
---
# <a name="oid_wwan_pco"></a>OID_WWAN_PCO

OID_WWAN_PCO は、モデムがモバイルオペレーターネットワークから受信したプロトコル構成オプション t (PCO) 値の状態とペイロードを報告します。 モデムから返される PCO 値は、ポート番号によって OID 要求構造に指定されている PDN に対応します。

クエリ要求の場合、モデムは最初にこの OID を受信したときに NDIS_STATUS_INDICATION_REQUIRED に応答します。 クエリ要求が完了すると、 [NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)構造を含む[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知が返されます。 **NDIS_WWAN_PCO_STATUS**には、pco ステータスと pco 値を表す[WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value)構造体が含まれます。

Set 要求は適用できません。

## <a name="remarks"></a>注釈

Microsoft 受信トレイのミニポートクラスドライバーを使用してホストからクエリ要求を受信するモデムの場合、モデムは**MBIM_CID_DEVICE_SERVICES**クエリに応答するときに、 **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**サービスの新しい**MBIM_CID_PCO** CID (index = 9) をサポートしていることを通知する必要があります。 *MBIM_CID_PCO*の詳細については、「 [MB プロトコル構成オプション (pco) 操作](mb-protocol-configuration-options-pco-operations.md)」を参照してください。

Microsoft 受信トレイのミニポートクラスドライバーを使用しないモデムの場合、WWANSVC からクエリ要求を受信するには、モデムのミニポートドライバーが、 [OID OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)クエリ要求に応答するときに*WWAN_OPTIONAL_SERVICE_CAPS_PCO*オプションをサポートすることを通知する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1709**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[**WWAN_PCO_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB プロトコル構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
