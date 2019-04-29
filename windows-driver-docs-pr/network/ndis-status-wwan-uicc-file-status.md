---
title: NDIS_STATUS_WWAN_UICC_FILE_STATUS
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_UICC_FILE_STATUS クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_UICC_FILE_STATUS 通知を使用します。
ms.assetid: ABC19EDC-E414-4783-BC3B-ECABDF06C0C5
ms.date: 04/09/2019
keywords: -NDIS_STATUS_WWAN_UICC_FILE_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3d5044299d100217d61e26fa8a96e8510a3100e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384639"
---
# <a name="ndisstatuswwanuiccfilestatus"></a>NDIS_STATUS_WWAN_UICC_FILE_STATUS

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_UICC_FILE_STATUS**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)クエリ要求.

要請されていないイベントは適用されません。

この通知を使用して、 [ **NDIS_WWAN_UICC_FILE_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
