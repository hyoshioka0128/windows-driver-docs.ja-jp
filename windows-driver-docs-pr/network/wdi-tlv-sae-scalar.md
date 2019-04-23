---
title: WDI_TLV_SAE_SCALAR
description: WDI_TLV_SAE_SCALAR では、同時認証の Equals (SAE) コミット要求の有限フィールド要素 (FFE) を含む TLV です。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_SCALAR ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a83799cb55108cf95583122f280ac0cf188841d3
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905409"
---
# <a name="wditlvsaescalar"></a>WDI_TLV_SAE_SCALAR

**WDI_TLV_SAE_SCALAR**同時認証の Equals (SAE) コミット要求の有限フィールド要素 (FFE) を含む TLV は、します。

この TLV がで使用される[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x153

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | FFE します。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
