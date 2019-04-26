---
title: OID_WWAN_MPDP
description: OID_WWAN_MPDP は、プライマリの PDP コンテキスト/EPS ベアラーを表す MB デバイスの複数のパケット データ プロトコル (MPDP) インターフェイスに関する情報を照会または設定します。
ms.assetid: 2A8E496A-212A-4999-A82C-9B97CEEC2C7E
keywords:
- OID_WWAN_MPDP、MPDP OID
ms.date: 06/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 757b96d735e332cdbf265fd5b37f8515133b2bc7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353729"
---
# <a name="oidwwanmpdp"></a>OID_WWAN_MPDP

OID_WWAN_MPDP は、プライマリの PDP コンテキスト/EPS ベアラーを表す MB デバイスの複数のパケット データ プロトコル (MPDP) インターフェイスに関する情報を照会または設定します。

クエリ要求を処理、ミニポート ドライバー応答 MB サービスに非同期的に NDIS_STATUS_INDICATION_REQUIRED を最初に返すことでします。 クエリ要求が完了した後に、ドライバーが送信、 [NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)で書式設定された、プライマリの PDP コンテキストの子インターフェイスの一覧を含む通知が、 [ **NDIS_WWAN_MPDP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)構造体。

セットの要求のようにクエリ要求のミニポート ドライバー応答 MB サービスに非同期的に NDIS_STATUS_INDICATION_REQUIRED を最初に返すことによってします。 セットの要求が含まれています、 [ **NDIS_WWAN_SET_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)を格納する構造体、 [ **NDIS_WWAN_MPDP_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)操作の情報を持つ構造体。 

場合、**操作**のメンバー、 **NDIS_WWAN_MPDP_INFO**構造に設定されている**WwanMPDPOperationCreateChildInterface**、クライアント ドライバーは、新しい子インターフェイスを作成します。プライマリの PDP コンテキスト。 MB サービスに、操作が成功した場合、新しく作成された子インターフェイスの GUID と、この操作の状態の結果が返されます、 [ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造体含まれている、 [NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知します。

場合、**操作**のメンバー、 **NDIS_WWAN_MPDP_INFO**構造に設定されている**WwanMPDPOperationDeleteChildInterface**、対応するミニポート ドライバーを削除します以前に作成され MB サービスに、削除操作に関する情報を返します子インターフェイス、 [ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造に含まれている、 [NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知します。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1809 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)

[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)

[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)

[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)

[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)

[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)

[*EvtMbbDeviceCreateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)
