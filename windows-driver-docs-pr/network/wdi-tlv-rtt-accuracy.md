---
title: WDI_TLV_RTT_ACCURACY
description: WDI_TLV_RTT_ACCURACY は、ラウンドトリップ時間 (RTT) の測定値に対する精度または予想される近さの程度を含む TLV です。これは、タイミング測定 (FTM) 要求の真の値になります。
ms.assetid: 689C9C22-6AA4-4581-BF26-147F49F2456F
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_RTT_ACCURACY
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6c238e844fab98c883aef76ca995a4bafc92f46b
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917486"
---
# <a name="wdi_tlv_rtt_accuracy"></a>WDI_TLV_RTT_ACCURACY

**WDI_TLV_RTT_ACCURACY**は、ラウンドトリップ時間 (RTT) の測定値に対する精度または予想される近さの程度を含む TLV です。これは、タイミング測定 (FTM) 要求の真の値になります。 単位は、のようになります。

たとえば、現在の RTT が 66712.82 (ターゲット AP から10メートル離れた) である場合、ハードウェアプロファイルによって、測定が +/-1 メーターによってオフにされていることがわかっている場合、RTT 精度は6671.28 のようになります。 実際の FTM が作成されたときのハードウェアのプロファイルと照合条件に基づいて、可能な限り正確な精度を提供するのは、IHV の役割です。 FTM の精度に影響を与える変数が複数あり、これらの変数を測定して考慮できる複数の可能性があります。 より具体的な精度が求められる理由は、これが、位置を計算するときに高い精度で測定を優先する場合や、FTM 精度に基づいて計算された位置エラーを変更する場合など、上位層で使用できる有用な情報であるためです。 プロファイリングを行う場合は、少なくとも90% の CDF を使用する必要があります。 

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15D

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
