---
title: WDI_TLV_CANCEL_PARAMETERS
description: WDI_TLV_CANCEL_PARAMETERS は、OID_WDI_ABORT_TASK のパラメーターを含む TLV です。
ms.assetid: 7C071743-5DF9-4CA8-873A-64B06C94388F
ms.date: 07/18/2017
keywords:
- WDI_TLV_CANCEL_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 904134a226fe0eccfa9d7d7cb29d586b35d91428
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578929"
---
# <a name="wditlvcancelparameters"></a>WDI\_TLV\_キャンセル\_パラメーター


WDI\_TLV\_キャンセル\_パラメーターはパラメーターを含む TLV [OID\_WDI\_中止\_タスク](https://msdn.microsoft.com/library/windows/hardware/dn925835)します。

## <a name="tlv-type"></a>TLV 型


0x2B

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                   | 説明                                             |
|------------------------|---------------------------------------------------------|
| NDIS\_OID              | 元のタスクを中止してから OID を指定します。 |
| UINT32                 | 元のタスクのトランザクション ID を指定します。    |
| WDI\_ポート\_ID (UINT16) | 元のタスクからポートの ID を指定します。           |

 

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

 

 




