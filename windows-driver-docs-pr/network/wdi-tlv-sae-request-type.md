---
title: WDI_TLV_SAE_REQUEST_TYPE
description: WDI_TLV_SAE_REQUEST_TYPE は、ターゲットの BSSID に送信する Equals (SAE) 要求フレームの同時認証の種類を含む TLV です。
ms.assetid: 90F0F7DA-DACA-49EF-86E8-CE4206D83882
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_REQUEST_TYPE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b7031c2121a376bb199fe94fdf2c1ef73f126b92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841740"
---
# <a name="wdi_tlv_sae_request_type"></a>WDI_TLV_SAE_REQUEST_TYPE

**WDI_TLV_SAE_REQUEST_TYPE**は、ターゲットの BSSID に送信する EQUALS (SAE) 要求フレームの同時認証の種類を含む TLV です。

この TLV は、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のコマンドパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14F

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) | BSSID に送信する SAE 要求フレームの種類。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
