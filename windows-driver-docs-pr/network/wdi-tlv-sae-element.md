---
title: WDI_TLV_SAE_ELEMENT
description: WDI_TLV_SAE_ELEMENT は、Equals (SAE) Commit 要求を同時に認証するための、エンコードされたフィールド要素 (EFE) を含む TLV です。
ms.assetid: B5E4DC7A-40B5-4F1D-A1C5-D2526FA0DF4D
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_ELEMENT
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1244433d21a586bb425964f9adfee38e95899272
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916386"
---
# <a name="wdi_tlv_sae_element"></a>WDI_TLV_SAE_ELEMENT

**WDI_TLV_SAE_ELEMENT**は、EQUALS (SAE) Commit 要求を同時に認証するための、エンコードされたフィールド要素 (efe) を含む TLV です。

この TLV は[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x154

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | EFE の一部。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
