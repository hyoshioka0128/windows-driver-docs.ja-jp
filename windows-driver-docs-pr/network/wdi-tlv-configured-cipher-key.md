---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY は、OID_WDI_GET_PM_PROTOCOL_OFFLOAD で設定する構成済みの暗号のリストを含む TLV です。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- WDI_TLV_CONFIGURED_CIPHER_KEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3a568784b252013a5f7a803612755c176087f2c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528803"
---
# <a name="wditlvconfiguredcipherkey"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY 設定する構成済みの暗号のリストを含む TLV [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)します。 ドライバーは、現在構成されている GTK または iGTK キーを返す必要があります。 この TLV の値であり、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV します。

## <a name="tlv-type"></a>TLV 型

0x147

## <a name="length"></a>長さ

次の値のバイト単位でサイズ。

## <a name="values"></a>値

| 種類 | 説明 |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_key_type) | 返されるキーの型。 |
| [WDI_CIPHER_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | このキーを使用する暗号アルゴリズムを指定します。 |
| UINT8\[6\] | 初期の 48 ビット値のパケット数 (PN)、再生の保護のために使用します。 省略可能な場合**CipherAlgorithm**は**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**します。 |
| TLV &LT; 一覧\<UINT8 &GT;&GT; | 存在する場合、場合にのみ**CipherAlgorithm**は**WDI_CIPHER_ALGO_CCMP**します。 CCMP 暗号アルゴリズムのキーのデータが含まれています。 |
| TLV &LT; 一覧\<UINT8 &GT;&GT; | 存在する場合、場合にのみ**CipherAlgorithm**は**WDI_CIPHER_ALGO_GCMP**します。 GCMP 暗号アルゴリズムのキーのデータが含まれています。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | 存在する場合、場合にのみ**CipherAlgorithm**は**WDI_CIPHER_ALGO_TKIP**します。 |
| TLV &LT; 一覧\<UINT8 &GT;&GT; | 存在する場合、場合にのみ**CipherAlgorithm**は**WDI_CIPHER_ALGO_BIP**します。 |
| TLV &LT; 一覧\<UINT8 &GT;&GT; | 存在する場合、場合にのみ**CipherAlgorithm**は**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**します。 |
| TLV &LT; 一覧\<UINT8 &GT;&GT; | 存在する場合、場合にのみ**CipherAlgorithm**の範囲では**WDI_CIPHER_ALGO_IHV_START**に**WDI_CIPHER_ALGO_IHV_END**します。 |
 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
