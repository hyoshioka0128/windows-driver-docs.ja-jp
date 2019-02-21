---
title: WDI_TLV_P2P_GROUP_ID
description: WDI_TLV_P2P_GROUP_ID では、Wi-Fi Direct GO 用のグループ ID を含む TLV です。
ms.assetid: 5DF5E7AA-4A5A-4AF5-90E6-40791C8DBB56
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GROUP_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bdc87b13b3bdd8fe62cba53f8c92317f7316c79c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535366"
---
# <a name="wditlvp2pgroupid"></a>WDI\_TLV\_P2P\_グループ\_ID


WDI\_TLV\_P2P\_グループ\_ID は、Wi-Fi Direct GO 用のグループ ID を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x75

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                          |
|----------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI\_TLV\_P2P\_デバイス\_アドレス**](wdi-tlv-p2p-device-address.md) |                                |          | Wi-Fi Direct の移動のデバイスのアドレスを指定します。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid-list.md)                          |                                |          | グループの SSID を指定します。                            |

 

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

 

 




