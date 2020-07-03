---
title: WDI_TLV_SAE_SCALAR
description: WDI_TLV_SAE_SCALAR は、Equals (SAE) Commit 要求を同時に認証するための有限のフィールド要素 (FFE) を含む TLV です。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_SCALAR
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a5823b4f11a4b5d3bae1cba9afe173ed8572fca2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918102"
---
# <a name="wdi_tlv_sae_scalar"></a>WDI_TLV_SAE_SCALAR

**WDI_TLV_SAE_SCALAR**は、EQUALS (SAE) Commit 要求を同時に認証するための有限のフィールド要素 (ffe) を含む TLV です。

この TLV は[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x153

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | FFE。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
