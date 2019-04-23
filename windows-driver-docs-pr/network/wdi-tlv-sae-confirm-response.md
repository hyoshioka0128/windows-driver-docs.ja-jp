---
title: WDI_TLV_SAE_CONFIRM_RESPONSE
description: WDI_TLV_SAE_CONFIRM_RESPONSE では、同時認証の Equals (SAE) 確認応答のフレームを含む TLV です。
ms.assetid: 42ACD823-3FFB-442F-B81C-82446C3606FF
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_CONFIRM_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 994ffc57f0550dc5ec59e7ae9f1f262d4e2f64ee
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905350"
---
# <a name="wditlvsaeconfirmresponse"></a>WDI_TLV_SAE_CONFIRM_RESPONSE

**WDI_TLV_SAE_CONFIRM_RESPONSE**同時認証の Equals (SAE) 確認応答のフレームを含む TLV です。

この TLV がのペイロード データに使用される[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)します。

## <a name="tlv-type"></a>TLV 型

0x14E

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | SAE 確認応答フレーム。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
