---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_APP_LIST 通知を使用して、以前の OID_WWAN_UICC_APP_LIST クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_UICC_APP_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 207b3775a8fed3def19dc698a774d6da9971a025
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844813"
---
# <a name="ndis_status_wwan_uicc_app_list"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_APP_LIST**通知を使用して、以前の[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)
