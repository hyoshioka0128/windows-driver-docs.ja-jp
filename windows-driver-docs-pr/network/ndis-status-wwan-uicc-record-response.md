---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_UICC_ACCESS_RECORD クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知を使用します。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3154bb247695748503a912aea42cc8d66ace21ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384636"
---
# <a name="ndisstatuswwanuiccrecordresponse"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)クエリまたは、要求を設定します。

要請されていないイベントは適用されません。

この通知を使用して、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
