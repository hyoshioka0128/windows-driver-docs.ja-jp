---
title: WDI_TLV_P2P_PERSISTENT_GROUP_ID
description: WDI_TLV_P2P_PERSISTENT_GROUP_ID では、接続に使用する永続的なグループのグループ ID を含む TLV です。
ms.assetid: 0C759D34-3197-4CAB-A691-187BC3457C04
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PERSISTENT_GROUP_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5b8a7db06565f3ae0122394d86c78be8e453a375
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529493"
---
# <a name="wditlvp2ppersistentgroupid"></a>WDI\_TLV\_P2P\_持続\_グループ\_ID


WDI\_TLV\_P2P\_持続\_グループ\_ID は、接続に使用する永続的なグループのグループ ID を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xF1

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                            |
|----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_P2P\_デバイス\_アドレス**](wdi-tlv-p2p-device-address.md) |                                |          | グループの所有者のデバイスのアドレス。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md)                               |                                |          | SSID のグループです。                        |

 

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

 

 




