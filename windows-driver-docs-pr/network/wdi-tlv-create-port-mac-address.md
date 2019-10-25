---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS は、OID_WDI_TASK_CREATE_PORT の MAC アドレスを含む TLV です。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_MAC_ADDRESS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: efadf719fc3ceb0da04249b425b2a256351e6cea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833843"
---
# <a name="wdi_tlv_create_port_mac_address"></a>WDI\_TLV\_\_ポート\_MAC\_アドレスを作成する


WDI\_TLV\_CREATE\_PORT\_MAC\_ADDRESS は、 [OID\_WDI\_タスク\_\_ポートを作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)するための mac アドレスを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xD9

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ポートの作成に使用する MAC アドレス。 |

 

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

 

 




