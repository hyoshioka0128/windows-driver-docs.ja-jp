---
title: NDIS_STATUS_WWAN_UICC_FILE_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_UICC_FILE_STATUS 通知を使用して、以前の OID_WWAN_UICC_FILE_STATUS クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: ABC19EDC-E414-4783-BC3B-ECABDF06C0C5
ms.date: 04/09/2019
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_UICC_FILE_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6a235c5a4f6e7a54e307c9cf6097956a1360eeaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844811"
---
# <a name="ndis_status_wwan_uicc_file_status"></a>NDIS_STATUS_WWAN_UICC_FILE_STATUS

ミニポートドライバーは、 **NDIS_STATUS_WWAN_UICC_FILE_STATUS**通知を使用して、以前の[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
