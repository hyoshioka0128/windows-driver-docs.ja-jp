---
title: WDI_TLV_RTT
description: WDI_TLV_RTT では、細かいタイミング測定 (FTM) 要求のピコで測定されたラウンドト リップ時間 (RTT) を含む TLV です。
ms.assetid: 82543997-30D3-469B-8EDE-31AF528BDDE4
ms.date: 02/15/2019
keywords:
- WDI_TLV_RTT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4584bfefa92829d249502e4ebf11816ef06a6390
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905288"
---
# <a name="wditlvrtt"></a>WDI_TLV_RTT

**WDI_TLV_RTT**ピコ、細かいタイミング測定 (FTM) 要求が、測定のラウンドト リップ時間 (RTT) を含む TLV します。 

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15C

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT32 | RTT します。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
