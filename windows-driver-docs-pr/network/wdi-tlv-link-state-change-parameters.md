---
title: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS
description: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE のリンク状態変更パラメーターを含む TLV です。
ms.assetid: 808C2E69-B713-41A3-AFB9-7441D2A96867
ms.date: 07/18/2017
keywords:
- WDI_TLV_LINK_STATE_CHANGE_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 0867d99ccc6fdd2269860eab892061460d63a0c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845057"
---
# <a name="wdi_tlv_link_state_change_parameters"></a>WDI\_TLV\_LINK\_の状態\_変更\_パラメーター


WDI\_TLV\_LINK\_状態\_変更\_パラメーターは、NDIS\_STATUS のリンク状態変更パラメーターを含む TLV で\_\_[リンク\_状態\_を変更](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-link-state-change)します。

## <a name="tlv-type"></a>TLV 型


0x56

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | リモートピアの MAC アドレスを指定します。                                                                                                                                   |
| UINT32                                            | 現在の TX リンク速度を指定します。 これは、この仮想ポートの現在の TX リンク速度である1秒あたりのキロビット数です。 変換は、1 kbps = 1000 bps です。 |
| UINT32                                            | 現在の RX リンク速度を指定します。 これは、この仮想ポートの現在の RX リンク速度である1秒あたりのキロビット数です。 変換は、1 kbps = 1000 bps です。 |
| UINT8                                             | 現在のリンクの品質を指定します。 この仮想ポートの現在のリンクの品質を示す 0 ~ 100 の値です。                                               |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




