---
title: OID_WDI_SET_SAE_AUTH_PARAMS
description: OID_WDI_SET_SAE_AUTH_PARAMS は、ドライバーからの NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED の通知に応答して WDI によって送信されます。 これには、Equals (SAE) コミットまたは Confirm 要求の同時認証を送信するために必要なパラメーター、または BSSID で SAE を実行できなかったことを示すエラーメッセージが含まれています。
ms.assetid: D20F92F9-8AEF-456C-B27A-20E61F75B3B7
ms.date: 02/15/2019
keywords:
- OID_WDI_SET_SAE_AUTH_PARAMS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6e465d32aaaa9abc398752498193ec423dcdaf40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843871"
---
# <a name="oid_wdi_set_sae_auth_params"></a>OID_WDI_SET_SAE_AUTH_PARAMS

**OID_WDI_SET_SAE_AUTH_PARAMS**は、ドライバーからの[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)の通知に応答して WDI によって送信されます。 これには、Equals (SAE) コミットまたは Confirm 要求の同時認証を送信するために必要なパラメーター、または BSSID で SAE を実行できなかったことを示すエラーメッセージが含まれています。 

このコマンドは、直接 OID 要求としてドライバーに送信されます。

SAE 認証の詳細については、「 [WPA3 SAE authentication](wpa3-sae-authentication.md)」を参照してください。

## <a name="command-parameters"></a>コマンドパラメーター

| TLV | タスクバーの検索ボックスに | 複数の TLV インスタンスを使用できます | オプション | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |  | AP の BSSID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) |   |   | BSSID に送信する SAE 要求フレームの種類。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | WDI_SAE_COMMIT_REQUEST |  | X | SAE Commit 要求パラメーター。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | WDI_SAE_CONFIRM_REQUEST |  | X | SAE Confirm 要求パラメーター。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 認証エラーの状態。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Dot11wdi |
