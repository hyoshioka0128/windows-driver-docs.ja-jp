---
title: OID_WWAN_LTE_ATTACH_STATUS
description: OID_WWAN_LTE_ATTACH_STATUS が最後に使用される LTE の OS の接続コンテキストを通知するために使用されます。
ms.assetid: 394650CF-5410-40C6-8749-D941DF68D303
ms.date: 08/23/2018
keywords: -OID_WWAN_LTE_ATTACH_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7a1355569f886c606cbf9c5e3cef5710a81a8303
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579880"
---
# <a name="oidwwanlteattachstatus"></a>OID_WWAN_LTE_ATTACH_STATUS

OID_WWAN_LTE_ATTACH_STATUS は LTE 接続コンテキストを最後に使用される既定の OS に通知するために使用されます。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md)通知含む、 [ **NDIS_WWAN_LTE_ATTACH_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)最後に使用される既定 LTE を記述する構造体は、コンテキストをアタッチします。

要求のセットには適用されません。

## <a name="remarks"></a>コメント

詳細については、この OID を使用して、[MBIM_CID_MS_LTE_ATTACH_STATUS](mb-lte-attach-operations.md)を参照してください。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチの操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
