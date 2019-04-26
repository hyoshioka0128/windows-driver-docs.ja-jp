---
title: WDI_TLV_RTT_VARIANCE
description: WDI_TLV_RTT_VARIANCE では、1 つ以上の測定を使用した場合、問題ありませんタイミング測定 (FTM) 要求中にラウンドト リップ時間 (RTT) を計算するために使用する測定値の統計的変位を含む TLV です。
ms.assetid: F8032726-4CC8-40F4-8FA1-840A3514A4B0
ms.date: 02/15/2019
keywords:
- WDI_TLV_RTT_VARIANCE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b19cf7aad3f6cc9c70f245628018679882458dc1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359088"
---
# <a name="wditlvrttvariance"></a>WDI_TLV_RTT_VARIANCE

**WDI_TLV_RTT_VARIANCE**は 1 つ以上の測定を使用した場合、問題ありませんタイミング測定 (FTM) 要求中にラウンドト リップ時間 (RTT) を計算するために使用する測定値の統計的変位を含む TLV します。 

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15E

## <a name="length"></a>長さ

Uint64 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT64 | RTT を計算するために使用する測定値の統計的分散。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
