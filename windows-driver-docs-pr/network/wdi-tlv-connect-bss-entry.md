---
title: WDI_TLV_CONNECT_BSS_ENTRY
description: WDI_TLV_CONNECT_BSS_ENTRY が、候補の一覧を含む TLV BSS エントリに接続します。
ms.assetid: 0D74B2DE-9224-4FDF-8EA8-B22CEC0B5F26
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECT_BSS_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a1a86fe448f113dc8b59fffaddca2e586f0085da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342907"
---
# <a name="wditlvconnectbssentry"></a>WDI\_TLV\_CONNECT\_BSS\_エントリ


WDI\_TLV\_CONNECT\_BSS\_エントリが候補の一覧を含む TLV BSS エントリに接続します。

## <a name="tlv-type"></a>TLV 型


0x34

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                   |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                    |                                |          | BSS の BSSID します。                                                                                                                                         |
| [**WDI\_TLV\_プローブ\_応答\_フレーム**](wdi-tlv-probe-response-frame.md)                    |                                | x        | プローブ応答フレーム。 プローブの応答を受信しなかった場合は、空がなります。                                                                        |
| [**WDI\_TLV\_ビーコン\_フレーム**](wdi-tlv-beacon-frame.md)                                     |                                | x        | ビーコン フレーム。 ビーコンを受信しなかった場合は、空がなります。                                                                                        |
| [**WDI\_TLV\_BSS\_エントリ\_信号\_情報**](wdi-tlv-bss-entry-signal-info.md)                 |                                |          | この BSS エントリのシグナルの情報。                                                                                                                    |
| [**WDI\_TLV\_BSS\_エントリ\_チャネル\_情報**](wdi-tlv-bss-entry-channel-info.md)               |                                |          | この BSS エントリのチャネル情報。                                                                                                                   |
| [**WDI\_TLV\_BSS\_エントリ\_デバイス\_コンテキスト**](wdi-tlv-bss-entry-device-context.md)           |                                | x        | IHV は、このピアに関するコンテキスト データを提供します。                                                                                                                |
| [**WDI\_TLV\_PMKID**](wdi-tlv-pmkid.md)                                                    |                                | x        | この BSS エントリの 16 バイト PMKID 値。                                                                                                                   |
| [**WDI\_TLV\_余分な\_アソシエーション\_要求\_IES**](wdi-tlv-extra-association-request-ies.md) |                                | x        | (再) に含まれる IE この BSSID の関連付け要求フレーム。 存在する場合、共通の IE に加えて含まれていますがあります。                  |
| [**WDI\_TLV\_FT\_初期\_ASSOC\_パラメーター**](wdi-tlv-ft-initial-assoc-parameters.md)     |                                | x        | 初期のモビリティ ドメイン関連パラメーター。                                                                                                           |
| [**WDI\_TLV\_FT\_REASSOC\_パラメーター**](wdi-tlv-ft-reassoc-parameters.md)                  |                                | x        | 迅速な移行のパラメーター (MDIE、R0KH ID、PMKR0Name、SNonce)。 これは、(初期モビリティ ドメインの関連付け) 中ではなくのみ高速切り替え存在します。 |
| [**WDI\_TLV\_BSS\_選択\_パラメーター**](wdi-tlv-bss-selection-parameters.md)            |                                | x        | [**WDI\_BSS\_選択\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/mt297629) BSS 選択範囲のホストによって使用される情報を提供します。                               |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




