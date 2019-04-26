---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS では、同時認証の Equals (SAE) 認証エラーのエラー状態を含む TLV です。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ac6d86e9fcfd81c3ec98da9b331938434845f5d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359036"
---
# <a name="wditlvsaestatus"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**同時認証の Equals (SAE) 認証エラーのエラー状態を含む TLV です。

この TLV がのコマンド パラメーターで使用される[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のペイロード データ内と[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)します。

## <a name="tlv-type"></a>TLV 型

0x14C

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) | 認証失敗を SAE エラー ステータスです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
