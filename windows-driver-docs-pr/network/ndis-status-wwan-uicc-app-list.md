---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_APP_LIST 通知を使用して、前の OID_WWAN_UICC_APP_LIST クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_UICC_APP_LIST
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6a5529db14a1c79be548c6d993557aecddd5e187
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916636"
---
# <a name="ndis_status_wwan_uicc_app_list"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_APP_LIST**通知を使用して、前の[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)
