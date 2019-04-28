---
title: WDI_TLV_ADDITIONAL_BEACON_IES
description: WDI_TLV_ADDITIONAL_BEACON_IES では、追加のビーコン IEs を含む TLV です。
ms.assetid: 7B4D863A-1480-4283-A5E9-5F4F043B0CDE
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADDITIONAL_BEACON_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 63f36e5cc676fd3a165a5efeb4c78868c1741db4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380562"
---
# <a name="wditlvadditionalbeaconies"></a>WDI\_TLV\_追加\_ビーコン\_IES


WDI\_TLV\_追加\_ビーコン\_IES は追加ビーコン IEs を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x98

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | ビーコン IEs の配列。 Wi-Fi Direct のポートはグループの所有者として動作しているときにビーコン パケットにこれらの追加 IEs を追加する必要があります。 これらには、Wi-Fi Direct のポートはデバイスまたはクライアントのモードで動作しているときは無視されます。 |

 

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

 

 




