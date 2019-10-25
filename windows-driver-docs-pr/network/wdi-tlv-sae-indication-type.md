---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE は、ターゲットの BSSID で SAE 認証を続行するために必要な情報の種類を含む TLV、または認証を続行できないことを通知します。
ms.assetid: F505CA27-4B2F-4210-8BE4-F3B931B86DDC
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_INDICATION_TYPE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 62c64663611e2f77b9ddb5955b1351d96d3938ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841743"
---
# <a name="wdi_tlv_sae_indication_type"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE**は、ターゲットの BSSID で SAE 認証を続行するために必要な情報の種類を含む TLV、または認証を続行できないことを通知します。

この TLV は、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)のペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14B

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) | ターゲットの BSSID で認証を続行するために必要な情報の種類、または認証を続行できないことを示す通知 SAE。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
