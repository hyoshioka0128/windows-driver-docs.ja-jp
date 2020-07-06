---
title: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
description: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
ms.assetid: 3BD36C57-BEE3-4BC8-BDF3-480E4066777A
ms.date: 02/14/2019
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 41e68102ae84897c7c7500c5c09f5d300245346e
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968319"
---
# <a name="ndis_status_wdi_indication_sae_auth_params_needed"></a>NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED

Wi-fi アダプターは、Equals (SAE) 認証を同時に認証するための要求パラメーターにこの通知を送信します。

ミニポートドライバーがターゲットの BSSID で SAE 認証を実行するように要求された場合、認証のさまざまな段階で情報を要求する必要があります。 最初は、コミット要求フレームのパラメーターを要求し、成功した場合は Confirm 要求フレームを要求します。 ドライバーで回復不可能なタイムアウトまたはエラーが発生した場合は、OS にも示されます。

この通知は、SAE 認証プロセス中に送信されます。 詳細については、「 [WPA3-SAE authentication](wpa3-sae-authentication.md)」を参照してください。

## <a name="payload-data"></a>ペイロードデータ

| TLV | Type | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | AP の BSS ID。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) |   |   | BSSID で認証を続行するために必要な情報の種類、または認証を続行できないことを示す通知 SAE。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | TLV\<LIST\<UINT8>> |   | X | SAE コミット応答フレーム。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | TLV\<LIST\<UINT8>> |   | X | SAE Confirm 応答フレーム。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 認証エラーの状態。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1903

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

