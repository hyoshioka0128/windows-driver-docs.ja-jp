---
title: WDI_TLV_BAND_CHANNEL
description: WDI_TLV_BAND_CHANNEL では、指定されたバンドをスキャンするチャネルを含む TLV です。
ms.assetid: CC3142BE-45CC-4064-A203-ADAF5BE05C01
ms.date: 07/18/2017
keywords:
- WDI_TLV_BAND_CHANNEL ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b57992389745cb57d3b1b329ba11f37769e58fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361788"
---
# <a name="wditlvbandchannel"></a>WDI\_TLV\_バンド\_チャネル


WDI\_TLV\_バンド\_チャネルは、指定されたバンドをスキャンするチャネルを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x2C

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                     |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BANDID**](wdi-tlv-bandid.md)                         |                                |          | バンドの識別子を指定します。                                                          |
| [**WDI\_TLV\_チャネル\_情報\_一覧**](wdi-tlv-channel-info-list.md) |                                |          | スキャンするチャネルのリストを指定します。 リストが空の場合、ポートがすべてのチャンネルでスキャンする必要があります。 |

 

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

 

 




