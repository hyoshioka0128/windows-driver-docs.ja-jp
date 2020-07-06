---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
description: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB は、IHV ドライバーから受信したデバイスサービスに関する情報を含む TLV です。
ms.assetid: D07CDC24-849F-447A-8447-FD2D37178C42
ms.date: 06/15/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
ms.localizationpriority: medium
ms.openlocfilehash: 53ed36aa0bc80fdb79c114211d97d7a9864946e7
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968441"
---
# <a name="wdi_tlv_device_service_params_data_blob"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB

WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB は、IHV ドライバーから受信したデバイスサービスに関する情報を含む TLV です。 この TLV は、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態表示で使用されます。

## <a name="tlv-type"></a>TLV 型

0x141

## <a name="length"></a>長さ

のサイズ (バイト単位) `(UINT8 * (the number of elements in the list))` 。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| TLV\<List\<UINT8\>\> | OptionalIHV ドライバーから受信した情報。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1809

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

