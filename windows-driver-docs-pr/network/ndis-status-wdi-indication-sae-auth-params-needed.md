---
title: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
description: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
ms.assetid: 3BD36C57-BEE3-4BC8-BDF3-480E4066777A
ms.date: 02/14/2019
keywords:
- NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 76caa33f1e808bc802446488fcffb4ba994a1a96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361046"
---
# <a name="ndisstatuswdiindicationsaeauthparamsneeded"></a>NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED

Wi-fi アダプターは、同時認証の Equals (SAE) 認証の要求パラメーターにこの通知を送信します。

SAE 認証ターゲット BSSID を実行するミニポート ドライバーが要求されると、その認証のさまざまな段階で情報を要求する必要があります。 最初に、し、確認要求フレームに成功した場合、コミット要求フレームのパラメーターを要求します。 ドライバーには、回復不可能なタイムアウトかエラーが発生すると、そのことも示して、OS に。

この通知は、SAE の認証プロセス中に送信されます。 詳細については、次を参照してください。 [WPA3 SAE 認証](wpa3-sae-authentication.md)します。

## <a name="payload-data"></a>ペイロード データ

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | AP の BSS ID。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_indication_type) |   |   | BSSID、または通知 SAE 認証を続行するために必要な情報の種類、認証を続行できません。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | TLV\<一覧\<UINT8 &GT;&GT; |   | x | SAE コミット応答フレーム。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | TLV\<一覧\<UINT8 &GT;&GT; |   | x | SAE 確認応答フレーム。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) |   | x | 認証失敗を SAE エラー ステータスです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
