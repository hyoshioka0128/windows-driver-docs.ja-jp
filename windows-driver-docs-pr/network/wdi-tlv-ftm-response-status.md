---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS は、ターゲット BSS からのタイミング測定 (FTM) 応答ステータスを含む TLV です。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_FTM_RESPONSE_STATUS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 64444f4a79a6aeef786346ac0aa838c4c7a39b86
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917344"
---
# <a name="wdi_tlv_ftm_response_status"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS**は、ターゲット BSS からのタイミング測定 (FTM) 応答ステータスを含む TLV です。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x159

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) | FTM 応答の状態。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
