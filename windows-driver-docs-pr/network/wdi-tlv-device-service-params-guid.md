---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
description: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID では、この状態を示す値が属している、デバイス サービスを識別する GUID を含む TLV です。
ms.assetid: BBD64E6F-A2E2-4601-A231-4FCB4574EFC7
ms.date: 06/15/2018
keywords:
- WDI_TLV_DEVICE_SERVICE_PARAMS_GUID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0a07ccc43724f11b6d29c2c7bb29f8bc313f2f0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571739"
---
# <a name="wditlvdeviceserviceparamsguid"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_GUID

WDI_TLV_DEVICE_SERVICE_PARAMS_GUID では、この状態を示す値が属している、デバイス サービスを識別する GUID を含む TLV です。 この TLV がで使用される、 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状態を示す値。

## <a name="tlv-type"></a>TLV 型

0x140

## <a name="length"></a>長さ

GUID のバイト単位のサイズ。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| GUID | この状態の表示が所属する (IHV と OEM によって定義される) と、デバイス サービスを識別する GUID。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 Version 1809 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
