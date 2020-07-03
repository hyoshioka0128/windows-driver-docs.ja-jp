---
title: WDI_TLV_RTT_VARIANCE
description: WDI_TLV_RTT_VARIANCE は、複数の測定が使用されている場合に、問題のあるタイミング測定 (FTM) 要求でラウンドトリップ時間 (RTT) を計算するために使用される測定値の統計的分散を含む TLV です。
ms.assetid: F8032726-4CC8-40F4-8FA1-840A3514A4B0
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_RTT_VARIANCE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ae8edd015d9bb17ab8cdb2fe383569665ce9be5a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918228"
---
# <a name="wdi_tlv_rtt_variance"></a>WDI_TLV_RTT_VARIANCE

**WDI_TLV_RTT_VARIANCE**は、複数の測定が使用されている場合に、問題のあるタイミング測定 (FTM) 要求でラウンドトリップ時間 (RTT) を計算するために使用される測定値の統計的分散を含む TLV です。 

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15E

## <a name="length"></a>長さ

UINT64 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT64 | RTT の計算に使用される測定値の統計的分散。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
