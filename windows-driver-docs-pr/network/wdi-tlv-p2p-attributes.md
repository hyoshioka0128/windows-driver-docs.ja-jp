---
title: WDI_TLV_P2P_ATTRIBUTES
description: WDI_TLV_P2P_ATTRIBUTES では、Wi-Fi Direct 属性を含む TLV です。
ms.assetid: 2EC99A30-3D2F-4552-A763-B77E030B5CE5
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 757d6df8982cff18c5e7d556f9b41acd884d32a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571407"
---
# <a name="wditlvp2pattributes"></a>WDI\_TLV\_P2P\_属性


WDI\_TLV\_P2P\_属性は、Wi-Fi Direct 属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x25

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                       |
|---------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI\_TLV\_P2P\_機能**](wdi-tlv-p2p-capabilities.md)                       |                                |          | Wi-Fi Direct 機能。                    |
| [**WDI\_TLV\_P2P\_インターフェイス\_アドレス\_一覧**](wdi-tlv-p2p-interface-address-list.md) |                                |          | Wi-Fi Direct インターフェイスの MAC アドレスの配列。 |

 

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

 

 




