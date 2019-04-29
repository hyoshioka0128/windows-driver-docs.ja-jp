---
title: NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_UICC_ACCESS_BINARY クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE 通知を使用します。
ms.assetid: DA4EAA85-C24F-42FC-98D7-075F49A35672
ms.date: 04/10/2019
keywords: -NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 64957bf1d68b0b4d61858537a1330cee5217e109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384638"
---
# <a name="ndisstatuswwanuiccbinaryresponse"></a>NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)クエリまたは、要求を設定します。

要請されていないイベントは適用されません。

この通知を使用して、 [ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
