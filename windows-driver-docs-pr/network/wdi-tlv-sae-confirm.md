---
title: WDI_TLV_SAE_CONFIRM
description: WDI_TLV_SAE_CONFIRM では、同時認証の Equals (SAE) 確認要求の確認入力 フィールドを含む TLV です。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_CONFIRM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 949cf66d9025d3912bb347119af532ec0b9d152b
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905457"
---
# <a name="wditlvsaeconfirm"></a>WDI_TLV_SAE_CONFIRM

**WDI_TLV_SAE_CONFIRM**同時認証の Equals (SAE) 確認要求の確認入力 フィールドを含む TLV です。

この TLV がで使用される[WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x157

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | 確認入力 フィールドにします。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
