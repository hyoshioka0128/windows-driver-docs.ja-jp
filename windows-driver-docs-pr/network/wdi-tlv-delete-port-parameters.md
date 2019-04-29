---
title: WDI_TLV_DELETE_PORT_PARAMETERS
description: WDI_TLV_DELETE_PORT_PARAMETERS は、OID_WDI_TASK_DELETE_PORT のパラメーターを含む TLV です。
ms.assetid: F3DDECDC-1A92-4022-9E2C-780ED480172C
ms.date: 07/18/2017
keywords:
- WDI_TLV_DELETE_PORT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b9623fdc7dfaf098ccd6791f3aa6185973ab730d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331831"
---
# <a name="wditlvdeleteportparameters"></a>WDI\_TLV\_削除\_ポート\_パラメーター


WDI\_TLV\_削除\_ポート\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_削除\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925950).

## <a name="tlv-type"></a>TLV 型


0x2A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                          |
|--------|--------------------------------------|
| UINT16 | 削除するポート番号を指定します。 |

 

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

 

 




