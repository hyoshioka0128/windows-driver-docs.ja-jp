---
title: WDI_TLV_CONNECT_BSS_ENTRY
description: WDI_TLV_CONNECT_BSS_ENTRY は、候補の接続 BSS エントリの一覧を含む TLV です。
ms.assetid: 0D74B2DE-9224-4FDF-8EA8-B22CEC0B5F26
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECT_BSS_ENTRY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 7ea2332b18377c8f467096d56ca28d98e32c93d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843389"
---
# <a name="wdi_tlv_connect_bss_entry"></a>WDI\_TLV\_接続\_BSS\_エントリ


WDI\_TLV\_CONNECT\_BSS\_ENTRY は、候補となる接続 BSS エントリの一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x34

## <a name="length"></a>長さ


含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                                        | 複数の TLV インスタンスを使用できます | オプション | 説明                                                                                                                                                   |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                    |                                |          | BSS の BSSID。                                                                                                                                         |
| [**WDI\_TLV\_プローブ\_応答\_フレーム**](wdi-tlv-probe-response-frame.md)                    |                                | X        | プローブ応答フレーム。 プローブ応答を受信していない場合、これは空になります。                                                                        |
| [**WDI\_TLV\_ビーコン\_フレーム**](wdi-tlv-beacon-frame.md)                                     |                                | X        | ビーコンフレーム。 ビーコンが受信されていない場合、これは空になります。                                                                                        |
| [**WDI\_TLV\_BSS\_ENTRY\_SIGNAL\_INFO**](wdi-tlv-bss-entry-signal-info.md)                 |                                |          | この BSS エントリのシグナル情報。                                                                                                                    |
| [**WDI\_TLV\_BSS\_エントリ\_チャネル\_情報**](wdi-tlv-bss-entry-channel-info.md)               |                                |          | この BSS エントリのチャネル情報。                                                                                                                   |
| [**WDI\_TLV\_BSS\_ENTRY\_デバイス\_コンテキスト**](wdi-tlv-bss-entry-device-context.md)           |                                | X        | IHV がこのピアに関するコンテキストデータを提供しました。                                                                                                                |
| [**WDI\_TLV\_PMKID**](wdi-tlv-pmkid.md)                                                    |                                | X        | この BSS エントリの16バイト PMKID 値。                                                                                                                   |
| [**WDI\_TLV\_追加\_アソシエーション\_要求\_** ](wdi-tlv-extra-association-request-ies.md) |                                | X        | この BSSID の (re) アソシエーション要求フレームに含まれる IE。 存在する場合は、共通の IE に加えて追加する必要があります。                  |
| [**WDI\_TLV\_FT\_INITIAL\_ASSOC\_PARAMETERS**](wdi-tlv-ft-initial-assoc-parameters.md)     |                                | X        | 最初のモビリティドメインの関連付けパラメーター。                                                                                                           |
| [**WDI\_TLV\_FT\_REASSOC\_パラメーター**](wdi-tlv-ft-reassoc-parameters.md)                  |                                | X        | 高速移行パラメーター (MDIE、R0KH、PMKR0Name、SNonce)。 これは、(最初のモビリティドメインの関連付けではなく) 高速の移行の場合にのみ存在します。 |
| [**WDI\_TLV\_BSS\_SELECTION\_PARAMETERS**](wdi-tlv-bss-selection-parameters.md)            |                                | X        | [**WDI\_bss**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)は、ホストが bss 選択に使用する情報を提供する\_フラグを\_選択します。                               |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




