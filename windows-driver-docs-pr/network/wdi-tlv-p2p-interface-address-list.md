---
title: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST
description: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST では、Wi-Fi Direct インターフェイスのアドレス リストを含む TLV です。
ms.assetid: B7FCB047-28D2-43E2-B4D6-B24E7BC74D47
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INTERFACE_ADDRESS_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9d09ca2f457750358144b6fea1c10046331975b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353611"
---
# <a name="wditlvp2pinterfaceaddresslist"></a>WDI\_TLV\_P2P\_インターフェイス\_アドレス\_一覧


WDI\_TLV\_P2P\_インターフェイス\_アドレス\_リストは、Wi-Fi Direct インターフェイスのアドレス リストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x18

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 型                                                  | 説明                      |
|-------------------------------------------------------|----------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-fi MAC アドレスの配列。 |

 

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

 

 




