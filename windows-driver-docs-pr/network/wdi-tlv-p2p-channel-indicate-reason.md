---
title: WDI_TLV_P2P_CHANNEL_INDICATE_REASON
description: WDI_TLV_P2P_CHANNEL_INDICATE_REASON を示す値を送信するための理由を含む TLV です。
ms.assetid: DD746492-82C5-4458-94A2-778F7F0F30B4
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_INDICATE_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8ecbc2eab9601e56316fa4d58749ec461fe11c1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532654"
---
# <a name="wditlvp2pchannelindicatereason"></a>WDI\_TLV\_P2P\_チャネル\_を示す\_理由


WDI\_TLV\_P2P\_チャネル\_を示す\_理由を示す値を送信するための理由を含む TLV のです。

## <a name="tlv-type"></a>TLV 型


0x102

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 示す値を送信する理由です。 参照してください[ **WDI\_P2P\_チャネル\_を示す\_理由**](https://msdn.microsoft.com/library/windows/hardware/dn926090)の考えられる理由。 |

 

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

 

 




