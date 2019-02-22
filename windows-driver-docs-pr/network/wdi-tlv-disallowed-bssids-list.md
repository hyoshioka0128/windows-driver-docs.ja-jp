---
title: WDI_TLV_DISALLOWED_BSSIDS_LIST
description: WDI_TLV_DISALLOWED_BSSIDS_LIST では、関連付けに使用するのには許可されていない Bssid のリストを含む TLV です。
ms.assetid: A65A6C05-C4E1-4880-BF83-48B62D0C2FD3
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISALLOWED_BSSIDS_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ad8824c6a1264b3601d24fc52a8ebefb6c164373
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548722"
---
# <a name="wditlvdisallowedbssidslist"></a>WDI\_TLV\_許可しない\_BSSID\_一覧


WDI\_TLV\_許可しない\_BSSID\_リストは、関連付けに使用するのには許可されていない Bssid のリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xC3

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 種類                                                  | 説明                                                                                                                                               |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | 関連付けに使用するのには許可されていない Bssid の一覧。 アダプターがこの一覧にない任意の AP に関連付ける必要がありますいない場合、これを指定すると、 |

 

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

 

 




