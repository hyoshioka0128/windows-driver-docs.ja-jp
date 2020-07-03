---
title: WDI_TLV_SAE_CONFIRM
description: WDI_TLV_SAE_CONFIRM は、Equals (SAE) Confirm 要求を同時に認証するための Confirm フィールドを含む TLV です。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_CONFIRM
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a279d965e8df785a08aa1ff6c3c59189f2318d27
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918188"
---
# <a name="wdi_tlv_sae_confirm"></a>WDI_TLV_SAE_CONFIRM

**WDI_TLV_SAE_CONFIRM**は、EQUALS (SAE) CONFIRM 要求を同時に認証するための confirm フィールドを含む TLV です。

この TLV は[WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x157

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | Confirm フィールド。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
