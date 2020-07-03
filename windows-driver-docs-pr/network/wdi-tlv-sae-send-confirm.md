---
title: WDI_TLV_SAE_SEND_CONFIRM
description: WDI_TLV_SAE_SEND_CONFIRM は、Equals (SAE) Confirm 要求を同時に認証するための [送信の確認] フィールドを含む TLV です。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_SEND_CONFIRM
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 901946f9867bca33af52a4358ec041429c2c77d0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918288"
---
# <a name="wdi_tlv_sae_send_confirm"></a>WDI_TLV_SAE_SEND_CONFIRM

**WDI_TLV_SAE_SEND_CONFIRM**は、EQUALS (SAE) CONFIRM 要求を同時に認証するための [送信の確認] フィールドを含む TLV です。 [送信の確認] フィールドは、再生の再実行のカウンターとして使用されます。

この TLV は[WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x156

## <a name="length"></a>長さ

UINT16 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT16 | [送信の確認] フィールド。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
