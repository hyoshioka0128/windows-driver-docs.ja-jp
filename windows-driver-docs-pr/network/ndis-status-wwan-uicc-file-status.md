---
title: NDIS_STATUS_WWAN_UICC_FILE_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_FILE_STATUS 通知を使用して、前の OID_WWAN_UICC_FILE_STATUS クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: ABC19EDC-E414-4783-BC3B-ECABDF06C0C5
ms.date: 04/09/2019
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_UICC_FILE_STATUS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 09e6c1e4a2ad0e6c43ee8a2e121f9a685eab36d5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916631"
---
# <a name="ndis_status_wwan_uicc_file_status"></a>NDIS_STATUS_WWAN_UICC_FILE_STATUS

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_FILE_STATUS**通知を使用して、前の[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
