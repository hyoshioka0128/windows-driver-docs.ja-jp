---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS は、ターゲット BSS からのタイミング測定 (FTM) 応答ステータスを含む TLV です。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- WDI_TLV_FTM_RESPONSE_STATUS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 217b6714667aeefdf3606af1bd18277c7ab5c306
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844987"
---
# <a name="wdi_tlv_ftm_response_status"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS**は、ターゲット BSS からのタイミング測定 (FTM) 応答ステータスを含む TLV です。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x159

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) | FTM 応答の状態。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
