---
title: WDI_TLV_SAE_COMMIT_REQUEST
description: WDI_TLV_SAE_COMMIT_REQUEST では、同時認証の Equals (SAE) コミット要求のパラメーターを含む TLV です。
ms.assetid: E339E58E-7929-416A-815D-C663EF1359D4
ms.date: 02/14/2019
keywords:
- WDI_TLV_SAE_COMMIT_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 45946a0051d2bfe0e26aeeaa5dbc3f025e457cdc
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905420"
---
# <a name="wditlvsaecommitrequest"></a>WDI_TLV_SAE_COMMIT_REQUEST

**WDI_TLV_SAE_COMMIT_REQUEST**同時認証の Equals (SAE) コミット要求のパラメーターを含む TLV です。 

この TLV がのコマンド パラメーターで使用される[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)します。

## <a name="tlv-type"></a>TLV 型

0x150

## <a name="length"></a>長さ

すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | UINT16 |   |   | SAE 認証に使用される有限循環グループ。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | TLV\<一覧\<UINT8 &GT;&GT; |   |   | 有限フィールド要素 (FFE)。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | TLV\<一覧\<UINT8 &GT;&GT; |   |   | エンコードされたフィールドの要素 (EFE)。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | TLV\<一覧\<UINT8 &GT;&GT; |   |   | として、BSSID によって要求された反 clogging トークンです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
