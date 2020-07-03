---
title: WDI_TLV_SAE_CONFIRM_RESPONSE
description: WDI_TLV_SAE_CONFIRM_RESPONSE は、Equals (SAE) Confirm RESPONSE frame の同時認証を含む TLV です。
ms.assetid: 42ACD823-3FFB-442F-B81C-82446C3606FF
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_CONFIRM_RESPONSE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 071fbba63d0eb8dd5482eee99c63975d44922f25
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918190"
---
# <a name="wdi_tlv_sae_confirm_response"></a>WDI_TLV_SAE_CONFIRM_RESPONSE

**WDI_TLV_SAE_CONFIRM_RESPONSE**は、EQUALS (SAE) CONFIRM RESPONSE Frame の同時認証を含む TLV です。

この TLV は、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)のペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14E

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | SAE Confirm 応答フレーム。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
