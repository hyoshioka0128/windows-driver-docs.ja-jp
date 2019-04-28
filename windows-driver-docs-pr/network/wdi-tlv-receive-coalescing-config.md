---
title: WDI_TLV_RECEIVE_COALESCING_CONFIG
description: WDI_TLV_RECEIVE_COALESCING_CONFIG は、含む TLV は、結合の構成を受信します。
ms.assetid: 32542203-14DE-4F91-AB85-D2FA75ECAB9E
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_COALESCING_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ca82dfd24a199ca5180bb93d2139fd7f915e9c73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360193"
---
# <a name="wditlvreceivecoalescingconfig"></a>WDI\_TLV\_受信\_COALESCING\_構成


WDI\_TLV\_受信\_COALESCING\_構成が含む TLV は、結合の構成を受信します。

## <a name="tlv-type"></a>TLV 型


0 xdb

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                         |
|--------|---------------------------------------------------------------------|
| UINT32 | このフィルターに一致するパケットをキューに一意のキュー ID。            |
| UINT32 | 1 からサポートされているフィルターの数の値でフィルター ID。 |
| UINT32 | ミリ秒単位で結合の最大遅延。                       |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_受信\_COALESCING](https://msdn.microsoft.com/library/windows/hardware/dn925941)

 

 




