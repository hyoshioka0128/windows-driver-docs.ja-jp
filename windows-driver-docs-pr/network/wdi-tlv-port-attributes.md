---
title: WDI_TLV_PORT_ATTRIBUTES
description: WDI_TLV_PORT_ATTRIBUTES は、ポート属性を含む TLV です。
ms.assetid: F5A0BC8D-1B86-41C2-A530-860E15775695
ms.date: 07/18/2017
keywords:
- WDI_TLV_PORT_ATTRIBUTES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9809f4981f145124b4e1cdc16cb36030295407e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838009"
---
# <a name="wdi_tlv_port_attributes"></a>WDI\_TLV\_ポート\_属性


WDI\_TLV\_PORT\_ATTRIBUTES は、ポート属性を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x29

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                         |
|---------------------------------------------------|-----------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ポートに関連付けられている MAC アドレスを指定します。 |
| UINT16                                            | ポート番号を指定します。                          |

 

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

 

 




