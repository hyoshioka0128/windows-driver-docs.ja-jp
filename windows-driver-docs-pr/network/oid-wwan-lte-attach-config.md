---
title: OID_WWAN_LTE_ATTACH_CONFIG
description: OID_WWAN_LTE_ATTACH_CONFIG を使用すると、オペレーティングシステムは、挿入された SIM のプロバイダー (MCC/MNC ペア) の既定の LTE アタッチコンテキストを照会または設定できます。
ms.assetid: 7E753513-D6A2-4B67-9AED-83A695C39D3C
ms.date: 08/22/2018
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_LTE_ATTACH_CONFIG
ms.localizationpriority: medium
ms.openlocfilehash: bb13251a5d2ad8efaffb48de3995b640e19d1fc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843839"
---
# <a name="oid_wwan_lte_attach_config"></a>OID_WWAN_LTE_ATTACH_CONFIG

OID_WWAN_LTE_ATTACH_CONFIG を使用すると、オペレーティングシステムは、挿入された SIM のプロバイダー (MCC/MNC ペア) の既定の LTE アタッチコンテキストを照会または設定できます。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、 [NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)ステータス通知を送信する必要があります。このとき、後で、LTE アタッチ構成を記述する[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)構造を含む状態通知を送信します

セット要求の場合、この OID のペイロードには、設定するモデムの LTE アタッチコンテキスト情報を記述する[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)構造が含まれます。

## <a name="remarks"></a>注釈

各クエリまたは設定要求の後に、ミニポートドライバーは、LTE アタッチ構成を説明する[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)通知を返します。

この OID の使用方法の詳細については、「 [MBIM_CID_MS_LTE_ATTACH_CONFIG](mb-lte-attach-operations.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチ操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)

[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)
