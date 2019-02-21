---
title: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL
description: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL では、プローブ要求が探索時にリッスンのチャネルの属性を含めるかどうかを指定する TLV です。
ms.assetid: 75662669-102A-4186-951C-58D1B36D1686
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6d6527d30c3e51ef78f209bb4a3455f5874a18bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527737"
---
# <a name="wditlvp2pincludelistenchannel"></a>WDI\_TLV\_P2P\_INCLUDE\_リッスン\_チャネル


WDI\_TLV\_P2P\_INCLUDE\_リッスン\_チャネルは、プローブ要求が探索時にリッスンのチャネルの属性を含めるかどうかを指定する TLV します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x128

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                                                                                                           |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | このパラメーターは、プローブ要求が探索時にリッスンのチャネルの属性を含めるかどうかを指定します。 有効な値は 0 (含まれません) または 1 (が含まれます)。 |

 

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

 

 




