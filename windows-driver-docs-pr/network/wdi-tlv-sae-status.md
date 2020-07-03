---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS は、Equals (SAE) 認証エラーの状態の同時認証を含む TLV です。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_SAE_STATUS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d6ff2992c617a0b486db8023ec1f42682044fb42
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916833"
---
# <a name="wdi_tlv_sae_status"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**は、EQUALS (SAE) 認証エラーの状態の同時認証を含む TLV です。

この TLV は、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)の[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)およびペイロードデータのコマンドパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14C

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) | SAE 認証エラーの状態。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
