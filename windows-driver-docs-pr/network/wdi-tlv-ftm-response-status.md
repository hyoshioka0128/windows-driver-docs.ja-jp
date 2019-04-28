---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS では、ターゲット BSS から正しくタイミング測定 (FTM) 応答の状態を含む TLV です。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- WDI_TLV_FTM_RESPONSE_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ad6fe20d99fbf9ffcd408254297807dd9030ab5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382883"
---
# <a name="wditlvftmresponsestatus"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS**ターゲット BSS から正しくタイミング測定 (FTM) 応答の状態を含む TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x159

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ftm_response_status) | FTM 応答状態。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
