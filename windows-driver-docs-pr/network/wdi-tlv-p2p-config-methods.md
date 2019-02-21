---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS では、Wi-Fi Direct 構成メソッドを含む TLV です。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CONFIG_METHODS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5325763ad6396b8b0872fe3ec656aca91c7f5724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536378"
---
# <a name="wditlvp2pconfigmethods"></a>WDI\_TLV\_P2P\_CONFIG\_メソッド


WDI\_TLV\_P2P\_CONFIG\_メソッドは、Wi-Fi Direct 構成メソッドを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xEB

## <a name="length"></a>長さ


Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/dn898198)します。 暗証番号 (pin) の表示、暗証番号 (pin) のキーパッドおよび WFDS は適用できます。 |

 

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

 

 




