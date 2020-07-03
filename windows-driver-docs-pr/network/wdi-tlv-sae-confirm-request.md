---
title: WDI_TLV_SAE_CONFIRM_REQUEST
description: WDI_TLV_SAE_CONFIRM_REQUEST は、Equals (SAE) Confirm 要求を同時に認証するためのパラメーターを含む TLV です。
ms.assetid: 9E46D8BA-D359-45B3-8074-FA54F4618E71
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_CONFIRM_REQUEST
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 027ab43c85f4118fde80599b10f5fffa8601fd07
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918192"
---
# <a name="wdi_tlv_sae_confirm_request"></a>WDI_TLV_SAE_CONFIRM_REQUEST

**WDI_TLV_SAE_CONFIRM_REQUEST**は、EQUALS (SAE) CONFIRM 要求を同時に認証するためのパラメーターを含む TLV です。 

この TLV は、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のコマンドパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x151

## <a name="length"></a>長さ

含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値

| TLV | 型 | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | UINT16 |   |   | 再再生のカウンターとして使用される [確認の送信] フィールド。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | TLV\<LIST\<UINT8>> |  |   | Confirm フィールド。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
