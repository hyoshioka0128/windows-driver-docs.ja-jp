---
title: WDI_TLV_PHY_INFO
description: WDI_TLV_PHY_INFO は、PHY 情報を含む TLV です。
ms.assetid: 3A363FDC-FE79-42C4-AD19-A6B960857CBD
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e767a3e1dae77b38c8de8fdadca51c576e82f181
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569647"
---
# <a name="wditlvphyinfo"></a>WDI\_TLV\_PHY\_情報


WDI\_TLV\_PHY\_情報が PHY 情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x26

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                |
|----------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_PHY\_機能**](wdi-tlv-phy-capabilities.md)                  |                                |          | Phy 機能。      |
| [**WDI\_TLV\_PHY\_TX\_POWER\_レベル\_一覧**](wdi-tlv-phy-tx-power-level-list.md) |                                |          | テキサス州の電力レベルの一覧。 |
| [**WDI\_TLV\_PHY\_データ\_レート\_一覧**](wdi-tlv-phy-data-rate-list.md)            |                                |          | データの料金の一覧。      |

 

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

 

 




