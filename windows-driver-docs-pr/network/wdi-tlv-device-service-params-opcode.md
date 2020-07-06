---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE
description: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE は、デバイスサービス固有のオペコードを含む TLV です。
ms.assetid: A0C9E728-E0E5-47C1-AEB8-E001057FA35A
ms.date: 06/15/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE
ms.localizationpriority: medium
ms.openlocfilehash: 1c8a4ee4799d1ddcde2e41908afc28fa94541fea
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968193"
---
# <a name="wdi_tlv_device_service_params_opcode"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE

WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE は、デバイスサービス固有のオペコードを含む TLV です。 この TLV は、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態表示で使用されます。

## <a name="tlv-type"></a>TLV 型

0x13F

## <a name="length"></a>長さ

UINT8 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| TLV\<UINT8\> | デバイスサービス固有のオペコード。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1809

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

