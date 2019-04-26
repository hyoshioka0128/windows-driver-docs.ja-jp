---
title: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
description: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN では、同時認証の Equals (SAE) コミット要求の防止 clogging トークンを含む TLV です。
ms.assetid: 9A1046AE-029F-4B37-9523-655425BC93F1
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_ANTI_CLOGGING_TOKEN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6628de1eb463dbc774fa513fe7688b2e2e08bdfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359192"
---
# <a name="wditlvsaeanticloggingtoken"></a>WDI_TLV_SAE_ANTI_CLOGGING_TOKEN

**WDI_TLV_SAE_ANTI_CLOGGING_TOKEN**反 clogging 同時認証の Equals (SAE) コミット要求のトークンを含む TLV は、します。

この TLV がで使用される[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x155

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | 反 clogging トークンです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
