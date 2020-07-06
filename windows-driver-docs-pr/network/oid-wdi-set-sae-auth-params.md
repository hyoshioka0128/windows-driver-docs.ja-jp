---
title: OID_WDI_SET_SAE_AUTH_PARAMS
description: OID_WDI_SET_SAE_AUTH_PARAMS は、ドライバーからの NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED の通知に応答して WDI によって送信されます。 これには、Equals (SAE) コミットまたは Confirm 要求の同時認証を送信するために必要なパラメーター、または BSSID で SAE を実行できなかったことを示すエラーメッセージが含まれています。
ms.assetid: D20F92F9-8AEF-456C-B27A-20E61F75B3B7
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WDI_SET_SAE_AUTH_PARAMS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7895e12187c02675c21f1971f782f2cb1f8e8fc4
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968507"
---
# <a name="oid_wdi_set_sae_auth_params"></a>OID_WDI_SET_SAE_AUTH_PARAMS

**OID_WDI_SET_SAE_AUTH_PARAMS**は、ドライバーからの[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)の通知に応答して WDI によって送信されます。 これには、Equals (SAE) コミットまたは Confirm 要求の同時認証を送信するために必要なパラメーター、または BSSID で SAE を実行できなかったことを示すエラーメッセージが含まれています。 

このコマンドは、直接 OID 要求としてドライバーに送信されます。

SAE 認証の詳細については、「 [WPA3 SAE authentication](wpa3-sae-authentication.md)」を参照してください。

## <a name="command-parameters"></a>コマンド パラメーター

| TLV | Type | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |  | AP の BSSID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) |   |   | BSSID に送信する SAE 要求フレームの種類。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | WDI_SAE_COMMIT_REQUEST |  | X | SAE Commit 要求パラメーター。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | WDI_SAE_CONFIRM_REQUEST |  | X | SAE Confirm 要求パラメーター。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 認証エラーの状態。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1903

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

