---
title: WDI_TLV_STATION_ATTRIBUTES
description: WDI_TLV_STATION_ATTRIBUTES では、ステーションの属性を含む TLV です。
ms.assetid: CB15D3A4-5B42-44ED-A8A8-3E7F09B65F8B
ms.date: 07/18/2017
keywords:
- WDI_TLV_STATION_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 042d712e1358c72e3d80e711c451eda523c26d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559081"
---
# <a name="wditlvstationattributes"></a>WDI\_TLV\_ステーション\_属性


WDI\_TLV\_ステーション\_属性は、ステーションの属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x22

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                    |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------|
| [**WDI\_TLV\_ステーション\_機能**](wdi-tlv-station-capabilities.md)                     |                                |          | ステーションの機能。                      |
| [**WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧**](wdi-tlv-unicast-algorithm-list.md)                |                                | X        | サポートされているユニキャスト アルゴリズム。              |
| [**WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_一覧**](wdi-tlv-multicast-data-algorithm-list.md) |                                | X        | マルチキャスト データがサポートされているアルゴリズムです。       |
| [**WDI\_TLV\_マルチキャスト\_MGMT\_アルゴリズム\_一覧**](wdi-tlv-multicast-mgmt-algorithm-list.md) |                                | X        | マルチキャストのサポートされている管理アルゴリズム。 |

 

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

 

 




