---
title: WDI_TLV_RTT_ACCURACY
description: WDI_TLV_RTT_ACCURACY では、精度、または正常タイミング測定 (FTM) 要求の true 値にラウンドト リップ時間 (RTT) の測定、近さの程度の期待される範囲を含む TLV です。
ms.assetid: 689C9C22-6AA4-4581-BF26-147F49F2456F
ms.date: 02/15/2019
keywords:
- WDI_TLV_RTT_ACCURACY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a765cae38c9c1f153d5dcd54e94c176e7470dd45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359096"
---
# <a name="wditlvrttaccuracy"></a>WDI_TLV_RTT_ACCURACY

**WDI_TLV_RTT_ACCURACY**正確さ、または正常タイミング測定 (FTM) 要求の true 値にラウンドト リップ時間 (RTT) の測定、近さの程度の期待される範囲を含む TLV は、します。 単位は、ピコで。

などの場合は、現在の RTT、RTT 精度は 6671.28 ピコ 1 メートルの場合は、+/-で、測定をオフに可能性がありますをハードウェア プロファイルを介して 66712.82 ピコ (10 m 離れてターゲット AP) が呼ばれます。 可能な精度が実際の FTM を実行したときに、そのハードウェアと一致する条件のプロファイルに基づいて特定として提供する IHV の役目です。 FTM 精度に影響を与える複数の変数があると、これらの変数を複数の可能性を測定しと見なされます。 特定の精度が望ましい理由の位置を計算するときより高い精度で、または FTM の精度に基づく位置の計算エラーを変更するための測定値を優先など、上位層で使用できる有用な情報は、このためです。 CDF を使用する必要があります最小の 90% をプロファイルするとき。 

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15D

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT32 | RTT します。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
