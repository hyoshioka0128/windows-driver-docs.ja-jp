---
title: WDI_TLV_SAE_ELEMENT
description: WDI_TLV_SAE_ELEMENT では、同時認証の Equals (SAE) コミット要求のエンコードされたフィールド要素 (EFE) を含む TLV です。
ms.assetid: B5E4DC7A-40B5-4F1D-A1C5-D2526FA0DF4D
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_ELEMENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 47bca20236a58cd367c28f87a947d54eeed7b123
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905406"
---
# <a name="wditlvsaeelement"></a>WDI_TLV_SAE_ELEMENT

**WDI_TLV_SAE_ELEMENT**同時認証の Equals (SAE) コミット要求のエンコードされたフィールド要素 (EFE) を含む TLV です。

この TLV がで使用される[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x154

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | EFE の一部です。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
