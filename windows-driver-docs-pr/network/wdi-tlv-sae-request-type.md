---
title: WDI_TLV_SAE_REQUEST_TYPE
description: WDI_TLV_SAE_REQUEST_TYPE は、target BSSID に送信する Equals (SAE) 要求フレームの同時認証の種類を含む TLV です。
ms.assetid: 90F0F7DA-DACA-49EF-86E8-CE4206D83882
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_REQUEST_TYPE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5212ff147a514237108f06389dcb8b7bdedf8de6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918106"
---
# <a name="wdi_tlv_sae_request_type"></a>WDI_TLV_SAE_REQUEST_TYPE

**WDI_TLV_SAE_REQUEST_TYPE**は、target BSSID に送信する EQUALS (SAE) 要求フレームの同時認証の種類を含む TLV です。

この TLV は、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のコマンドパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14F

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) | BSSID に送信する SAE 要求フレームの種類。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
