---
title: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
description: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.assetid: 95AB3325-9AE7-4F10-8E00-88D502E1A5C9
ms.date: 04/02/2018
keywords:
- NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ca0f0fd8c13d3de0c3835c6499637ae700c9222f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366404"
---
# <a name="ndisstatuswdiindicationcipherkeyupdated"></a>NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED

ミニポート ドライバーでは、キーが更新された暗号ことを示すためには、この通知を送信します。

この通知が送信されるは、ドライバーがあるないオフロード RSN GTK キー更新中にのみ (を使用して、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md)フィールドで、 [OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)コマンド)。 ドライバーは、現在 Rsn GTK キー更新のオフロード状態にあるかどうか、この方法で示す必要がありますいないを使用してクエリを実行する場合は、更新されたキー情報を許可する必要がありますが、 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)際のコマンドオフロード状態です。

たとえば、ドライバーまたはファームウェア WNM スリープ モードの応答で新しい GTK/iGTK を受信する場合に、この通知を送信は。

## <a name="payload-data"></a>ペイロード データ

| 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS](wdi-tlv-pm-protocol-rsn-offload-keys.md) |   |   | 現在構成されている Rsn Eapol キー情報。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
