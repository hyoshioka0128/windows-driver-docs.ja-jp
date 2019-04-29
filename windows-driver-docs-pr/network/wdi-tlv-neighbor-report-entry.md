---
title: WDI_TLV_NEIGHBOR_REPORT_ENTRY
description: WDI_TLV_NEIGHBOR_REPORT_ENTRY では、近隣ノードのレポートを含む TLV です。
ms.assetid: 23A0AA84-3EDA-4D6F-9140-2361C0CF55AA
ms.date: 07/18/2017
keywords:
- WDI_TLV_NEIGHBOR_REPORT_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0ee93407c51e05707e3828f91ab3f77f378bc650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392276"
---
# <a name="wditlvneighborreportentry"></a>WDI\_TLV\_近隣\_レポート\_エントリ


WDI\_TLV\_近隣\_レポート\_エントリが近隣ノードのレポートを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x123

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                          | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                         |
|---------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                      |                                |          | 近隣ノードのレポートでアジア太平洋の BSSID します。                         |
| [**WDI\_TLV\_BSSID\_情報**](wdi-tlv-bssid-info.md)           |                                |          | AP の BSSID 情報。                                    |
| [**WDI\_TLV\_オペレーティング\_クラス**](wdi-tlv-operating-class.md) |                                |          | この BSSID によって示される AP の動作クラスです。              |
| [**WDI\_TLV\_チャネル\_数**](wdi-tlv-channel-number.md)   |                                |          | 最後既知オペレーティング AP のチャネル、この BSSID によって示されます。 |
| [**WDI\_TLV\_PHY\_型**](wdi-tlv-phy-type.md)               |                                |          | この BSSID によって示される AP の PHY 型。                     |

 

<a name="requirements"></a>必要条件
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

 

 




