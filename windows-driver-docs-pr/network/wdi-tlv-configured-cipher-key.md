---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY は、TLV に設定される構成済みの暗号の一覧を含むです。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- WDI_TLV_CONFIGURED_CIPHER_KEY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 659d6a2731bd403174beaa4e97c5540f0ec756cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844504"
---
# <a name="wdi_tlv_configured_cipher_key"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY は、TLV に設定される構成済みの暗号の一覧を含む[です。](oid-wdi-get-pm-protocol-offload.md) ドライバーは、現在構成されている GTK または iGTK キーを返す必要があります。 この TLV は、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV の値です。

## <a name="tlv-type"></a>TLV 型

0x147

## <a name="length"></a>長さ

次の値のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type) | 返されるキーの型。 |
| [WDI_CIPHER_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | このキーを使用する暗号アルゴリズムを指定します。 |
| UINT8\[6\] | 再生保護に使用されるパケット番号 (PN) の最初の48ビット値。 **CipherAlgorithm**が**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**の場合は省略可能です。 |
| TLV < LIST\<UINT8 > > | **CipherAlgorithm**が**WDI_CIPHER_ALGO_CCMP**の場合にのみ存在します。 CCMP 暗号アルゴリズムのキーデータを格納します。 |
| TLV < LIST\<UINT8 > > | **CipherAlgorithm**が**WDI_CIPHER_ALGO_GCMP**の場合にのみ存在します。 GCMP 暗号アルゴリズムのキーデータを格納します。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | **CipherAlgorithm**が**WDI_CIPHER_ALGO_TKIP**の場合にのみ存在します。 |
| TLV < LIST\<UINT8 > > | **CipherAlgorithm**が**WDI_CIPHER_ALGO_BIP**の場合にのみ存在します。 |
| TLV < LIST\<UINT8 > > | **CipherAlgorithm**が**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**、または**WDI_CIPHER_ALGO_WEP**の場合にのみ存在します。 |
| TLV < LIST\<UINT8 > > | **CipherAlgorithm**が**WDI_CIPHER_ALGO_IHV_START**から**WDI_CIPHER_ALGO_IHV_END**までの範囲内にある場合にのみ存在します。 |
 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
