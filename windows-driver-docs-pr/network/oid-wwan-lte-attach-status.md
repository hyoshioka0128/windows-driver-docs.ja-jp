---
title: OID_WWAN_LTE_ATTACH_STATUS
description: OID_WWAN_LTE_ATTACH_STATUS は、最後に使用された LTE アタッチコンテキストを OS に通知するために使用されます。
ms.assetid: 394650CF-5410-40C6-8749-D941DF68D303
ms.date: 08/23/2018
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_LTE_ATTACH_STATUS
ms.localizationpriority: medium
ms.openlocfilehash: 9ba8296f592e77cd98f1a7b64ba09fd80446345a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843837"
---
# <a name="oid_wwan_lte_attach_status"></a>OID_WWAN_LTE_ATTACH_STATUS

OID_WWAN_LTE_ATTACH_STATUS は、最後に使用された既定の LTE アタッチコンテキストを OS に通知するために使用されます。

ミニポートドライバーは、クエリ要求を非同期的に処理し、その後、最後に使用された既定の LTE アタッチコンテキストを記述する[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)構造を含む[NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md)通知を送信する前に、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返す必要があります。

Set 要求は適用できません。

## <a name="remarks"></a>注釈

この OID の使用方法の詳細については、「 [MBIM_CID_MS_LTE_ATTACH_STATUS](mb-lte-attach-operations.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチ操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
