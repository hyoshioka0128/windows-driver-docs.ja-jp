---
title: WDI_TLV_BAND_INFO
description: WDI_TLV_BAND_INFO では、バンド情報を含む TLV です。
ms.assetid: 37F1CE39-5471-489A-8DA2-F058B631B31F
ms.date: 07/18/2017
keywords:
- WDI_TLV_BAND_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9b33eeff65813cddd6bb3df1698fceb938bd3872
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536967"
---
# <a name="wditlvbandinfo"></a>WDI\_TLV\_バンド\_情報


WDI\_TLV\_バンド\_情報が帯域内の情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x27

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                   |
|----------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_バンド\_機能**](wdi-tlv-band-capabilities.md)    |                                |          | Band の機能です。                 |
| [**WDI\_TLV\_PHY\_型\_一覧**](wdi-tlv-phy-type-list.md)           |                                |          | このバンドで有効な PHY 種類の一覧。       |
| [**WDI\_TLV\_チャネル\_一覧**](wdi-tlv-channel-list.md)              |                                |          | このバンドで有効なチャネル番号の一覧。 |
| [**WDI\_TLV\_チャネル\_幅\_一覧**](wdi-tlv-channel-width-list.md) |                                |          | チャネル幅 (mhz) の一覧               |

 

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

 

 




