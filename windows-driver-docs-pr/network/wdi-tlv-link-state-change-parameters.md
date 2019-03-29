---
title: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS
description: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS は、リンクの状態を含む TLV が NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE のパラメーターを変更します。
ms.assetid: 808C2E69-B713-41A3-AFB9-7441D2A96867
ms.date: 07/18/2017
keywords:
- WDI_TLV_LINK_STATE_CHANGE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f343df41fe54f377d58831b797273936808771fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582216"
---
# <a name="wditlvlinkstatechangeparameters"></a>WDI\_TLV\_リンク\_状態\_変更\_パラメーター


WDI\_TLV\_リンク\_状態\_変更\_パラメーターは、のリンクの状態変更のパラメーターを含む TLV [NDIS\_状態\_WDI\_INDICATION\_リンク\_状態\_変更](https://msdn.microsoft.com/library/windows/hardware/dn925638)します。

## <a name="tlv-type"></a>TLV 型


0x56

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | リモート ピアの MAC アドレスを指定します。                                                                                                                                   |
| UINT32                                            | 現在の TX リンク速度を指定します。 これは、この仮想ポートの現在の TX リンク速度である値、キロビット/秒、です。 変換では、1 kbps = 1000 bps です。 |
| UINT32                                            | 現在の RX リンク速度を指定します。 これは、この仮想ポートの現在の RX リンク速度である値、キロビット/秒、です。 変換では、1 kbps = 1000 bps です。 |
| UINT8                                             | 現在のリンクの品質を指定します。 これは、この仮想ポートの現在のリンクの品質である、0 ~ 100 の範囲の値です。                                               |

 

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

 

 




