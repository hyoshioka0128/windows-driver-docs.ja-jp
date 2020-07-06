---
title: OID_WWAN_MPDP
description: OID_WWAN_MPDP は、プライマリ PDP コンテキスト/EPS ベアラーを表す MB デバイスの複数パケットデータプロトコル (MPDP) インターフェイスに関する情報を設定または照会します。
ms.assetid: 2A8E496A-212A-4999-A82C-9B97CEEC2C7E
keywords:
- OID_WWAN_MPDP、MPDP OID
ms.date: 06/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 164d47ef3c906481b9dc29e0068d3f80249e0676
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968307"
---
# <a name="oid_wwan_mpdp"></a>OID_WWAN_MPDP

OID_WWAN_MPDP は、プライマリ PDP コンテキスト/EPS ベアラーを表す MB デバイスの複数パケットデータプロトコル (MPDP) インターフェイスに関する情報を設定または照会します。

クエリ要求の場合、ミニポートドライバーは、最初に NDIS_STATUS_INDICATION_REQUIRED を返すことによって、MB サービスに非同期に応答します。 クエリ要求が完了すると、ドライバーは、 [**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)構造で書式設定された、プライマリ PDP コンテキストの子インターフェイスの一覧を含む[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)通知を送信します。

クエリ要求の場合と同様に、set 要求の場合、最初に NDIS_STATUS_INDICATION_REQUIRED を返すことによって、ミニポートドライバーは MB サービスに非同期に応答します。 セット要求には[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)構造が含まれています。この構造体には、操作に関する情報を含む[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)構造体が含まれています。 

**NDIS_WWAN_MPDP_INFO**構造体の**操作**メンバーが**WwanMPDPOperationCreateChildInterface**に設定されている場合、クライアントドライバーは、プライマリ PDP コンテキスト用に新しい子インターフェイスを作成します。 操作が成功した場合の、新しく作成された子インターフェイスの GUID と共に、この操作の状態の結果は、 [NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知に含まれる[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造体の MB サービスに返されます。

**NDIS_WWAN_MPDP_INFO**構造体の**操作**メンバーが**WwanMPDPOperationDeleteChildInterface**に設定されている場合、ミニポートドライバーは、前に作成した対応する子インターフェイスを削除し、 [NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知に含まれる[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造で、削除操作に関する情報を MB サービスに返します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン1809

**ヘッダー**: Ntddndis (Ndis .h を含む)


## <a name="see-also"></a>関連項目

[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)

[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)

[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)

[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)

[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)

[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)

[*EvtMbbDeviceCreateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)
