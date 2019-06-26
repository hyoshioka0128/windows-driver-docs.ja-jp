---
title: WDI_TLV_P2P_LISTEN_STATE
description: WDI_TLV_P2P_LISTEN_STATE は、Wi-Fi Direct を含む TLV リッスン状態です。
ms.assetid: 66BDF96A-2B9D-4188-AFC8-465786924B47
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_LISTEN_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 69f336c090e7a494ec74113682e7ddcfa157c8e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355428"
---
# <a name="wditlvp2plistenstate"></a>WDI\_TLV\_P2P\_リッスン\_状態


WDI\_TLV\_P2P\_リッスン\_状態は、Wi-Fi Direct リッスン状態を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x81

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                         | 説明                            |
|--------------------------------------------------------------|----------------------------------------|
| [**WDI\_P2P\_リッスン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_listen_state) | 必要な Wi-Fi Direct の状態をリッスンします。 |

 

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

 

 




