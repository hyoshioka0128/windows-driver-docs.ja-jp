---
title: WDI_TLV_SAE_COMMIT_REQUEST
description: WDI_TLV_SAE_COMMIT_REQUEST は、Equals (SAE) Commit 要求を同時に認証するためのパラメーターを含む TLV です。
ms.assetid: E339E58E-7929-416A-815D-C663EF1359D4
ms.date: 02/14/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_COMMIT_REQUEST
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7a4fd25037f7c315de65fe7ed4eb04df750f0b0c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918196"
---
# <a name="wdi_tlv_sae_commit_request"></a>WDI_TLV_SAE_COMMIT_REQUEST

**WDI_TLV_SAE_COMMIT_REQUEST**は、EQUALS (SAE) COMMIT 要求を同時に認証するためのパラメーターを含む TLV です。 

この TLV は、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のコマンドパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x150

## <a name="length"></a>長さ

含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値

| TLV | 型 | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | UINT16 |   |   | SAE 認証に使用される有限の循環グループ。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | TLV\<LIST\<UINT8>> |   |   | 有限フィールド要素 (FFE)。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | TLV\<LIST\<UINT8>> |   |   | エンコードされたフィールド要素 (EFE)。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | TLV\<LIST\<UINT8>> |   |   | BSSID によって要求された輻輳トークン。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
