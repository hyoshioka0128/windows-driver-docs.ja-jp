---
title: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST
description: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST は、Wi-fi ダイレクトインターフェイスのアドレス一覧を含む TLV です。
ms.assetid: B7FCB047-28D2-43E2-B4D6-B24E7BC74D47
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INTERFACE_ADDRESS_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 37ce045777c0bf70a2b40d8f463a7c5f9b223f2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842759"
---
# <a name="wdi_tlv_p2p_interface_address_list"></a>WDI\_TLV\_P2P\_インターフェイス\_アドレス\_リスト


WDI\_TLV\_P2P\_INTERFACE\_ADDRESS\_LIST は、Wi-fi Direct インターフェイスのアドレス一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x18

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                  | 説明                      |
|-------------------------------------------------------|----------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-fi MAC アドレスの配列。 |

 

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

 

 




