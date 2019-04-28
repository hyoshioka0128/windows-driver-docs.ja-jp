---
title: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES
description: WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES では、プローブ応答 i が含まれる TLV です。
ms.assetid: BDEDAD4D-A35B-4AE9-BC90-184CD75002B2
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADDITIONAL_PROBE_RESPONSE_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0957337ce6c66e8cd9ab1bd86bc5329ff31b46d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382179"
---
# <a name="wditlvadditionalproberesponseies"></a>WDI\_TLV\_追加\_プローブ\_応答\_IES


WDI\_TLV\_追加\_プローブ\_応答\_IES はプローブ応答 i が含まれる TLV します。

## <a name="tlv-type"></a>TLV 型


0x93

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                                                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | プローブの応答での配列。 Wi-Fi Direct のポートは、Wi-Fi Direct デバイスまたはグループの所有者として動作しているときに、プローブ応答パケットをこれら追加 IEs を追加する必要があります。 このメンバーには、Wi-Fi Direct のポートは、クライアント モードで動作している場合は無視されます。 |

 

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

 

 




