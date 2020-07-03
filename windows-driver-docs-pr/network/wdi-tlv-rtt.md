---
title: WDI_TLV_RTT
description: WDI_TLV_RTT は、タイミング測定 (FTM) 要求の測定されたラウンドトリップ時間 (RTT) を TLV で表したものです。
ms.assetid: 82543997-30D3-469B-8EDE-31AF528BDDE4
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_RTT
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 65873dda02a98d87f3fca8318d5bff3111bcc1d6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918198"
---
# <a name="wdi_tlv_rtt"></a>WDI_TLV_RTT

**WDI_TLV_RTT**は、タイミング測定 (FTM) 要求の測定されたラウンドトリップ時間 (RTT) を TLV で表したものです。 

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15C

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
