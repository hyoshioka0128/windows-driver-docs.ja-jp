---
title: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
description: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS は、タイミング測定 (FTM) 要求のラウンドトリップ時間 (RTT) を指定するために使用される測定値を含む TLV です。
ms.assetid: C629B5F5-FB30-4808-A392-69150C5A2FA3
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7c53d4881f59ac0c13895b9f0578b34e9e02eeac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916145"
---
# <a name="wdi_tlv_ftm_number_of_measurements"></a>WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS

**WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS**は、タイミング測定 (FTM) 要求のラウンドトリップ時間 (RTT) を指定するために使用される測定値を含む TLV です。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15B

## <a name="length"></a>長さ

UINT16 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT16 | RTT を提供するために使用される測定値の数。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
