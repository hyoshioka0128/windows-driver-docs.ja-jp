---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS では、Wi-Fi Direct 構成メソッドを含む TLV です。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CONFIG_METHODS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b5e1d4c3807bc0cdf4f3303839bf9053b15790f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355103"
---
# <a name="wditlvp2pconfigmethods"></a>WDI\_TLV\_P2P\_CONFIG\_メソッド


WDI\_TLV\_P2P\_CONFIG\_メソッドは、Wi-Fi Direct 構成メソッドを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xEB

## <a name="length"></a>長さ


Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_wps_configuration_method)します。 暗証番号 (pin) の表示、暗証番号 (pin) のキーパッドおよび WFDS は適用できます。 |

 

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

 

 




