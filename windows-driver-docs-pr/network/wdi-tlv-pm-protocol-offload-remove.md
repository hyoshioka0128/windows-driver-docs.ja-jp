---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE は、プロトコルを含む TLV オフロード OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD を削除する ID です。
ms.assetid: BD74C9F7-6370-41D5-841F-6949D7748E30
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 779f047d2fef0119316cd945bfafbff74de34792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531739"
---
# <a name="wditlvpmprotocoloffloadremove"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_削除


WDI\_TLV\_PM\_プロトコル\_オフロード\_削除は、削除するプロトコルのオフロード ID を含む TLV [OID\_WDI\_セット\_削除\_PM\_プロトコル\_オフロード](https://msdn.microsoft.com/library/windows/hardware/dn925943)します。

## <a name="tlv-type"></a>TLV 型


0x6C

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                        |
|--------|------------------------------------|
| UINT32 | プロトコルのオフロード ID を指定します |

 

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

 

 




