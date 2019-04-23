---
title: OID_WWAN_NITZ
description: OID_WWAN_NITZ は、ネットワーク Id とタイム ゾーン (NITZ) 現在のネットワークの時刻をクエリに使用されます。
ms.assetid: 5AC5842E-CBD1-47E0-88D2-D3F58CC6F142
ms.date: 04/11/2019
keywords:
- OID_WWAN_NITZ ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9e46b361ddabc0a5f684ca4850972f0a2e99c614
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905380"
---
# <a name="oidwwannitz"></a>OID_WWAN_NITZ

OID_WWAN_NITZ は、ネットワーク Id とタイム ゾーン (NITZ) 現在のネットワークの時刻をクエリに使用されます。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)状態通知を含む[ **NDIS_WWAN_NITZ_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)ネットワークの現在の時刻とタイム ゾーンを記述する構造体。

要求のセットには適用されません。

## <a name="remarks"></a>注釈

この OID の使用状況に関する詳細については、次を参照してください。 [MB NITZ サポート](mb-nitz-support.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10、バージョンが 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB NITZ サポート](mb-nitz-support.md)

[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)
