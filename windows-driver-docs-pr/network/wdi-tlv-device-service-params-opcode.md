---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE
description: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE では、デバイス サービスに固有のオペコードを含む TLV です。
ms.assetid: A0C9E728-E0E5-47C1-AEB8-E001057FA35A
ms.date: 06/15/2018
keywords:
- WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 75c1152c85fb382c27db8610af7f735b156c2710
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559758"
---
# <a name="wditlvdeviceserviceparamsopcode"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE

WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE では、デバイス サービスに固有のオペコードを含む TLV です。 この TLV がで使用される、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態を示す値。

## <a name="tlv-type"></a>TLV 型

0x13F

## <a name="length"></a>長さ

UINT8 のバイト単位のサイズ。

## <a name="values"></a>値

| 種類 | 説明 |
| --- | --- |
| TLV\<UINT8\> | デバイス サービスに固有のオペコードにします。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 Version 1809 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
