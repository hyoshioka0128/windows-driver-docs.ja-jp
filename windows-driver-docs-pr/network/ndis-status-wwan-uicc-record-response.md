---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知を使用して、以前の OID_WWAN_UICC_ACCESS_RECORD クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bc3cb6f294734f3a8f77342f4835d8552c8bbf95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844805"
---
# <a name="ndis_status_wwan_uicc_record_response"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE**通知を使用して、以前の[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
