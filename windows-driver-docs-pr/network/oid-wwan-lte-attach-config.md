---
title: OID_WWAN_LTE_ATTACH_CONFIG
description: OID_WWAN_LTE_ATTACH_CONFIG により、オペレーティング システムはクエリまたはセット LTE 既定値が挿入された SIM のプロバイダー (MCC/mnc もペア) のコンテキストをアタッチします。
ms.assetid: 7E753513-D6A2-4B67-9AED-83A695C39D3C
ms.date: 08/22/2018
keywords: -OID_WWAN_LTE_ATTACH_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 157740fd5afd819823d8c015961595ac6ed8bec9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532112"
---
# <a name="oidwwanlteattachconfig"></a>OID_WWAN_LTE_ATTACH_CONFIG

OID_WWAN_LTE_ATTACH_CONFIG により、オペレーティング システムはクエリまたはセット LTE 既定値が挿入された SIM のプロバイダー (MCC/mnc もペア) のコンテキストをアタッチします。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)状態の通知含む、 [ **NDIS_WWAN_LTE_ATTACH_CONTEXTS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts) LTE を記述する構造体は、構成をアタッチします。

この OID のペイロードを含む、一連の要求について、 [ **NDIS_WWAN_SET_LTE_ATTACH_CONTEXT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context) LTE を記述する構造体は、モデムを設定するためのコンテキスト情報をアタッチします。

## <a name="remarks"></a>注釈

各クエリまたは一連の要求後に、ミニポート ドライバーを返す必要があります、 [NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md) LTE を示す通知が構成をアタッチします。

詳細については、この OID を使用して、[MBIM_CID_MS_LTE_ATTACH_CONFIG](mb-lte-attach-operations.md)を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチの操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)

[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)
