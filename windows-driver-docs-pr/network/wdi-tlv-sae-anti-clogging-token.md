---
title: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
description: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN は、Equals (SAE) コミット要求を同時に認証するための輻輳トークンを含む TLV です。
ms.assetid: 9A1046AE-029F-4B37-9523-655425BC93F1
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bf97fbce6360f1f7c2f4839b921cec220f0cb03d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916892"
---
# <a name="wdi_tlv_sae_anti_clogging_token"></a>WDI_TLV_SAE_ANTI_CLOGGING_TOKEN

**WDI_TLV_SAE_ANTI_CLOGGING_TOKEN**は、EQUALS (SAE) コミット要求を同時に認証するための輻輳トークンを含む TLV です。

この TLV は[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x155

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | 輻輳トークンです。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
