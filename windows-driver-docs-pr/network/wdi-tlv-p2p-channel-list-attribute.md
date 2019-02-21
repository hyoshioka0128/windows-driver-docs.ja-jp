---
title: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE
description: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE では、チャネルの一覧の属性を含む TLV です。
ms.assetid: 2378AC49-1530-45E2-A7C8-FEAF5E6CDBE5
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3a3d1a6570bee286b0b1b915b660e9bdd6712b2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550184"
---
# <a name="wditlvp2pchannellistattribute"></a>WDI\_TLV\_P2P\_チャネル\_一覧\_属性


WDI\_TLV\_P2P\_チャネル\_一覧\_属性は、チャネルの一覧の属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xD5

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                                                          | 許可されている複数の TLV インスタンス | 省略可能 | 説明              |
|-------------------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI\_TLV\_国\_リージョン\_一覧**](wdi-tlv-country-region-list.md)        |                                |          | 国/地域の一覧です。 |
| [**WDI\_TLV\_P2P\_チャネル\_エントリ\_一覧**](wdi-tlv-p2p-channel-entry-list.md) | X                              |          | チャネルのリスト。    |

 

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

 

 




