---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
description: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID は、この状態の表示が属するデバイスサービスを識別する GUID を含む TLV です。
ms.assetid: BBD64E6F-A2E2-4601-A231-4FCB4574EFC7
ms.date: 06/15/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
ms.localizationpriority: medium
ms.openlocfilehash: c74ec4cb17a859c78c5b8742ccd696a92244a7c1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968203"
---
# <a name="wdi_tlv_device_service_params_guid"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_GUID

WDI_TLV_DEVICE_SERVICE_PARAMS_GUID は、この状態の表示が属するデバイスサービスを識別する GUID を含む TLV です。 この TLV は、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態表示で使用されます。

## <a name="tlv-type"></a>TLV 型

0x140

## <a name="length"></a>長さ

GUID のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| GUID | この状態の表示が属するデバイスサービスを識別する GUID (IHV/OEM による定義による)。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1809

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

