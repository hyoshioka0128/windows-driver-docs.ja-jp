---
title: WDI_TLV_SET_CLEAR_RECEIVE_COALESCING
description: WDI_TLV_SET_CLEAR_RECEIVE_COALESCING は、OID_WDI_SET_CLEAR_RECEIVE_COALESCING のフィルター ID を含む TLV です。
ms.assetid: 4AF7A1A4-A1B4-48AD-9989-B9E317F93459
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_CLEAR_RECEIVE_COALESCING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8e87b85be1b6698c6fc8859be4b4d4c4857df244
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362814"
---
# <a name="wditlvsetclearreceivecoalescing"></a>WDI\_TLV\_設定\_クリア\_受信\_COALESCING


WDI\_TLV\_設定\_クリア\_受信\_COALESCING のフィルター ID を含む TLV [OID\_WDI\_設定\_クリア\_受信\_COALESCING](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-clear-receive-coalescing)します。

## <a name="tlv-type"></a>TLV 型


0x9B

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明           |
|--------|-----------------------|
| UINT32 | フィルターの ID。 |

 

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

 

 




