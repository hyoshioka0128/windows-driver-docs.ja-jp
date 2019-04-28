---
title: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
description: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS では、細かいタイミング測定 (FTM) 要求に対するラウンド トリップ時間 (RTT) を提供するために使用する測定値の数を含む TLV です。
ms.assetid: C629B5F5-FB30-4808-A392-69150C5A2FA3
ms.date: 02/15/2019
keywords:
- WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8ddb6d6a3db8d8d4755818084004f073d695b720
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382887"
---
# <a name="wditlvftmnumberofmeasurements"></a>WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS

**WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS**細かいタイミング測定 (FTM) 要求に対するラウンド トリップ時間 (RTT) を提供するために使用する測定値の数を含む TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15B

## <a name="length"></a>長さ

Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT16 | RTT を提供するために使用する測定値の数。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
