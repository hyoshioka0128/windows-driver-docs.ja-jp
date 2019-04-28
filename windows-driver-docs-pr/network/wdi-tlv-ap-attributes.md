---
title: WDI_TLV_AP_ATTRIBUTES
description: WDI_TLV_AP_ATTRIBUTES では、アクセス ポイントの属性を含む TLV です。
ms.assetid: FD6F635C-85FF-4668-AA17-12677A61F84D
ms.date: 07/18/2017
keywords:
- WDI_TLV_AP_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6630d830c214be4460dfc8fb7261ca3102f6286a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374554"
---
# <a name="wditlvapattributes"></a>WDI\_TLV\_AP\_属性


WDI\_TLV\_AP\_属性は、アクセス ポイントの属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x23

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                              |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------|
| [**WDI\_TLV\_AP\_機能**](wdi-tlv-ap-capabilities.md)                               |                                |          | アクセス ポイント機能です。           |
| [**WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧**](wdi-tlv-unicast-algorithm-list.md)                |                                |          | サポートされているユニキャスト アルゴリズム。        |
| [**WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_一覧**](wdi-tlv-multicast-data-algorithm-list.md) |                                |          | マルチキャスト データがサポートされているアルゴリズムです。 |

 

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

 

 




