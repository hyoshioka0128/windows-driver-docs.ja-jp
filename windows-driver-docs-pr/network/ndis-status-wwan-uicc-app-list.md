---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_UICC_APP_LIST クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_UICC_APP_LIST 通知を使用します。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -NDIS_STATUS_WWAN_UICC_APP_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f3ea5ed361af7250f198306dee9d0a04bdd8b331
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384641"
---
# <a name="ndisstatuswwanuiccapplist"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_UICC_APP_LIST**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)クエリ要求。

要請されていないイベントは適用されません。

この通知を使用して、 [ **NDIS_WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)
