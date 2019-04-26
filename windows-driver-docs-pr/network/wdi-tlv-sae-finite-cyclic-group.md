---
title: WDI_TLV_SAE_FINITE_CYCLIC_GROUP
description: WDI_TLV_SAE_FINITE_CYCLIC_GROUP では、同時認証の Equals (SAE) 認証のためコミット要求で有限の循環グループを含む TLV です。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_FINITE_CYCLIC_GROUP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 54002f71babf4c86ae05fb09a5899aa00910548b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359058"
---
# <a name="wditlvsaefinitecyclicgroup"></a>WDI_TLV_SAE_FINITE_CYCLIC_GROUP

**WDI_TLV_SAE_FINITE_CYCLIC_GROUP**同時認証の Equals (SAE) 認証のためコミット要求で有限の循環グループを含む TLV です。

この TLV がで使用される[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x152

## <a name="length"></a>長さ

Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT16 | SAE 認証に使用される有限循環グループ。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
