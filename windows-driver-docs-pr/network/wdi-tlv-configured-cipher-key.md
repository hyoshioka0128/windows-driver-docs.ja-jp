---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY は、OID_WDI_GET_PM_PROTOCOL_OFFLOAD で設定するように構成された暗号の一覧を含む TLV です。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_CONFIGURED_CIPHER_KEY
ms.localizationpriority: medium
ms.openlocfilehash: 4f106098a27d8256ebad5afc90bd508ef1f08686
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967943"
---
# <a name="wdi_tlv_configured_cipher_key"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY は、 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)で設定するように構成された暗号の一覧を含む TLV です。 ドライバーは、現在構成されている GTK または iGTK キーを返す必要があります。 この TLV は、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV の値です。

## <a name="tlv-type"></a>TLV 型

0x147

## <a name="length"></a>長さ

次の値のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type) | 返されるキーの型。 |
| [WDI_CIPHER_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | このキーを使用する暗号アルゴリズムを指定します。 |
| UINT8 \[ 6\] | 再生保護に使用されるパケット番号 (PN) の最初の48ビット値。 **CipherAlgorithm**が**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**の場合は省略可能です。 |
| TLV<リスト\<UINT8>> | **CipherAlgorithm**が**WDI_CIPHER_ALGO_CCMP**場合にのみ存在します。 CCMP 暗号アルゴリズムのキーデータを格納します。 |
| TLV<リスト\<UINT8>> | **CipherAlgorithm**が**WDI_CIPHER_ALGO_GCMP**場合にのみ存在します。 GCMP 暗号アルゴリズムのキーデータを格納します。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | **CipherAlgorithm**が**WDI_CIPHER_ALGO_TKIP**場合にのみ存在します。 |
| TLV<リスト\<UINT8>> | **CipherAlgorithm**が**WDI_CIPHER_ALGO_BIP**場合にのみ存在します。 |
| TLV<リスト\<UINT8>> | **CipherAlgorithm**が**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**の場合にのみ存在します。 |
| TLV<リスト\<UINT8>> | **CipherAlgorithm**が**WDI_CIPHER_ALGO_IHV_END** **WDI_CIPHER_ALGO_IHV_START**の範囲内にある場合にのみ存在します。 |
 

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1803

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

