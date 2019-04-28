---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE では、関連付け、Ethertype をカプセル化を含む TLV です。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- WDI_TLV_ETHERTYPE_ENCAP_TABLE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 09984b650f05b0c6b455ac3a308f1bc7a8cc1e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380868"
---
# <a name="wditlvethertypeencaptable"></a>WDI\_TLV\_ETHERTYPE\_全て\_テーブル


WDI\_TLV\_ETHERTYPE\_全て\_テーブルは、アソシエーションの Ethertype カプセル化を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x31

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                                       | 説明                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn897818)\[\] | 配列の[ **WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn897818)関連付け Ethertype カプセル化を指定する要素。 |

 

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

 

 




