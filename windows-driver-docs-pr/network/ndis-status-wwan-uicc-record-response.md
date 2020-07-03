---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知を使用して、前の OID_WWAN_UICC_ACCESS_RECORD クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 38c3944223468723a4baa626ccc54fcf89e340f5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916629"
---
# <a name="ndis_status_wwan_uicc_record_response"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE**通知を使用して、以前の[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
