---
title: OID_WDI_SET_SAE_AUTH_PARAMS
description: OID_WDI_SET_SAE_AUTH_PARAMS は、WDI NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED を示す値をドライバーからの応答で送信されます。 同時認証の Equals (SAE) コミットまたは確認要求、または、BSSID で SAE の実行の失敗を示すエラー メッセージを送信するために必要なパラメーターが含まれています。
ms.assetid: D20F92F9-8AEF-456C-B27A-20E61F75B3B7
ms.date: 02/15/2019
keywords:
- OID_WDI_SET_SAE_AUTH_PARAMS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 090fb0fe3d97293f250989526f608dbd19d0747e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348940"
---
# <a name="oidwdisetsaeauthparams"></a>OID_WDI_SET_SAE_AUTH_PARAMS

**OID_WDI_SET_SAE_AUTH_PARAMS** WDI によってへの応答で送信される、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)ドライバーからを示す値。 同時認証の Equals (SAE) コミットまたは確認要求、または、BSSID で SAE の実行の失敗を示すエラー メッセージを送信するために必要なパラメーターが含まれています。 

このコマンドは、ドライバーに直接 OID 要求として送信されます。

SAE 認証の詳細については、次を参照してください。 [WPA3 SAE 認証](wpa3-sae-authentication.md)します。

## <a name="command-parameters"></a>コマンドのパラメーター

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |  | AP の BSSID します。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_request_type) |   |   | BSSID に送信する SAE 要求フレームの型。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | WDI_SAE_COMMIT_REQUEST |  | x | SAE コミット要求パラメーターです。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | WDI_SAE_CONFIRM_REQUEST |  | x | SAE 確認要求パラメーターです。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) |   | x | SAE 認証エラーのエラー ステータスです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
