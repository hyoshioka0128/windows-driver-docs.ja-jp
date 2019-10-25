---
title: OID_WWAN_PCO
description: OID_WWAN_PCO は、オペレータネットワークからモデムが受信した PCO 値の状態とペイロードを報告します。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO、PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545a15e9b0291f83e426ab0264f9ed0dbe2afd3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843821"
---
# <a name="oid_wwan_pco"></a>OID_WWAN_PCO

OID_WWAN_PCO は、モデムが携帯電話会社のネットワークから受信したプロトコル構成オプション t (PCO) 値の状態とペイロードを報告します。 モデムから返される PCO 値は、ポート番号によって OID 要求構造に指定されている PDN に対応します。

クエリ要求の場合、モデムは最初にこの OID を受信したときに NDIS_STATUS_INDICATION_REQUIRED で応答します。 クエリ要求が完了すると、 [NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)構造体を含む[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知が返されます。 **NDIS_WWAN_PCO_STATUS**には、pco ステータスと pco 値を表す[WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value)構造体が含まれています。

Set 要求は適用できません。

## <a name="remarks"></a>注釈

Microsoft 受信トレイのミニポートクラスドライバーを使用してホストからクエリ要求を受信するモデムの場合、モデムは**MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**サービスで新しい**MBIM_CID_PCO** CID (index = 9) をサポートしていることを通知する必要があります。**MBIM_CID_DEVICE_SERVICES**クエリに応答する場合。 *MBIM_CID_PCO*の詳細については、「 [MB プロトコル構成オプション (pco) 操作](mb-protocol-configuration-options-pco-operations.md)」を参照してください。

Microsoft 受信トレイのミニポートクラスドライバーを使用しないモデムの場合、WWANSVC からクエリ要求を受信するために、モデムのミニポートドライバーは、OID OID_WWAN_ に応答するときに*WWAN_OPTIONAL_SERVICE_CAPS_PCO*オプションをサポートすることを通知する必要があります。 [DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)クエリ要求。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[**WWAN_PCO_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB プロトコル構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
