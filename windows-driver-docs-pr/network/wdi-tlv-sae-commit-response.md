---
title: WDI_TLV_SAE_COMMIT_RESPONSE
description: WDI_TLV_SAE_COMMIT_RESPONSE は、Equals (SAE) コミット応答フレームの同時認証を含む TLV です。
ms.assetid: 3E243737-F1C8-4554-96D2-E05C77DBA8B6
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_COMMIT_RESPONSE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7572824c416f8c687af9dbece137135b2063ff48
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918194"
---
# <a name="wdi_tlv_sae_commit_response"></a>WDI_TLV_SAE_COMMIT_RESPONSE

**WDI_TLV_SAE_COMMIT_RESPONSE**は、EQUALS (SAE) コミット応答フレームの同時認証を含む TLV です。

この TLV は、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)のペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14D

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | SAE コミット応答フレーム。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
