---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE は、ターゲットの BSSID での SAE 認証を続行するために必要な情報の種類を含む TLV です。認証を続行できないことを通知します。
ms.assetid: F505CA27-4B2F-4210-8BE4-F3B931B86DDC
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_INDICATION_TYPE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c18e537352aa073fac0e705986bd360d584b2daf
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916775"
---
# <a name="wdi_tlv_sae_indication_type"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE**は、ターゲットの BSSID での SAE 認証を続行するために必要な情報の種類を含む TLV です。認証を続行できないことを通知します。

この TLV は、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)のペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14B

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) | ターゲットの BSSID で認証を続行するために必要な情報の種類、または認証を続行できないことを示す通知 SAE。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
