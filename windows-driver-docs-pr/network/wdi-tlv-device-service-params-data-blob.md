---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
description: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB では、IHV ドライバーから受信したデバイスのサービスに関する情報を含む TLV です。
ms.assetid: D07CDC24-849F-447A-8447-FD2D37178C42
ms.date: 06/15/2018
keywords:
- WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 76bec883c708bb9976d907c119e0cc790e5b4e0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571040"
---
# <a name="wditlvdeviceserviceparamsdatablob"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB

WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB では、IHV ドライバーから受信したデバイスのサービスに関する情報を含む TLV です。 この TLV がで使用される、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態を示す値。

## <a name="tlv-type"></a>TLV 型

0x141

## <a name="length"></a>長さ

サイズ (バイト単位) の`(UINT8 * (the number of elements in the list))`します。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| TLV\<一覧\<UINT8\>\> | [省略可能]IHV ドライバーから受信した情報。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 Version 1809 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
