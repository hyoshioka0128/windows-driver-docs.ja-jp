---
title: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
description: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.assetid: 95AB3325-9AE7-4F10-8E00-88D502E1A5C9
ms.date: 04/02/2018
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 371bba94d65b738b4062cacab775fc2648783913
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968059"
---
# <a name="ndis_status_wdi_indication_cipher_key_updated"></a>NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED

ミニポートドライバーは、暗号キーが更新されたことを示すために、この通知を送信します。

この通知が送信されるのは、ドライバーが RSN GTK のキー更新を ( [OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)コマンドで登録されている[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md)を使用して) オフロードしていない場合のみです。 現在、ドライバーが Rsn GTK のキー更新のオフロード状態にある場合は、このメソッドを使用していることを示すことはできません。また、オフロード状態から出たときに、更新されたキー情報を[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)コマンドで照会することを許可する必要があります。

たとえば、ドライバーは、WNM-スリープモードの応答で新しい GTK/iGTK を受け取った場合に、この通知を送信します。

## <a name="payload-data"></a>ペイロードデータ

| Type | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS](wdi-tlv-pm-protocol-rsn-offload-keys.md) |   |   | 現在構成されている Rsn Eapol キー情報。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1803

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

