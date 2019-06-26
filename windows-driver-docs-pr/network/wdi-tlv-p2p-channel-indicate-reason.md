---
title: WDI_TLV_P2P_CHANNEL_INDICATE_REASON
description: WDI_TLV_P2P_CHANNEL_INDICATE_REASON を示す値を送信するための理由を含む TLV です。
ms.assetid: DD746492-82C5-4458-94A2-778F7F0F30B4
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_INDICATE_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 54a541a7741c529a2844c41b1189df8dfef3b519
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385705"
---
# <a name="wditlvp2pchannelindicatereason"></a>WDI\_TLV\_P2P\_チャネル\_を示す\_理由


WDI\_TLV\_P2P\_チャネル\_を示す\_理由を示す値を送信するための理由を含む TLV のです。

## <a name="tlv-type"></a>TLV 型


0x102

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 示す値を送信する理由です。 参照してください[ **WDI\_P2P\_チャネル\_を示す\_理由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_channel_indicate_reason)の考えられる理由。 |

 

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

 

 




