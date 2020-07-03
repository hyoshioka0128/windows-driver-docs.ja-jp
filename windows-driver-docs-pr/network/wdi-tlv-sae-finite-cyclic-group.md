---
title: WDI_TLV_SAE_FINITE_CYCLIC_GROUP
description: WDI_TLV_SAE_FINITE_CYCLIC_GROUP は、Equals (SAE) 認証の同時認証を行うためにコミット要求で使用される有限の循環グループを含む TLV です。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_FINITE_CYCLIC_GROUP
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cbeb5f051be1c84267f9036d984c908845630c81
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917132"
---
# <a name="wdi_tlv_sae_finite_cyclic_group"></a>WDI_TLV_SAE_FINITE_CYCLIC_GROUP

**WDI_TLV_SAE_FINITE_CYCLIC_GROUP**は、EQUALS (SAE) 認証の同時認証を行うためにコミット要求で使用される有限の循環グループを含む TLV です。

この TLV は[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x152

## <a name="length"></a>長さ

UINT16 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT16 | SAE 認証に使用される有限の循環グループ。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
