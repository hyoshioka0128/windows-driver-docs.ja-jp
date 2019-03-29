---
title: WDI_TLV_COALESCING_FILTER_MATCH_COUNT
description: WDI_TLV_COALESCING_FILTER_MATCH_COUNT は、一致したパケットの数を含む TLV 受信ネットワーク ポートのフィルターです。
ms.assetid: 9B9A1ED9-B842-4788-94C9-829876EB5D73
ms.date: 07/18/2017
keywords:
- WDI_TLV_COALESCING_FILTER_MATCH_COUNT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ea499ff0229bae2e18017c3468b98d8c47b11322
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571736"
---
# <a name="wditlvcoalescingfiltermatchcount"></a>WDI\_TLV\_COALESCING\_フィルター\_一致\_数


WDI\_TLV\_COALESCING\_フィルター\_一致\_数が一致したパケットの数を含む TLV 受信ネットワーク ポートでフィルターします。

## <a name="tlv-type"></a>TLV 型


0x66

## <a name="length"></a>長さ


サイズ (バイト単位) で、uint64 型。

## <a name="values"></a>値


| 型   | 説明                                                                  |
|--------|------------------------------------------------------------------------------|
| UINT64 | 一致したパケットの数には、ネットワーク ポートのフィルターが表示されます。 |

 

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

 

 




