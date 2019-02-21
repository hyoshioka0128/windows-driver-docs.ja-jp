---
title: WDI_TLV_NEXT_DIALOG_TOKEN
description: WDI_TLV_NEXT_DIALOG_TOKEN では、次のアクションのフレームで使用されるダイアログのトークンを含む TLV です。
ms.assetid: B11331CB-50D3-4A3B-93A5-359ABD918E70
ms.date: 07/18/2017
keywords:
- WDI_TLV_NEXT_DIALOG_TOKEN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9bc10eec5f6d557734ee2fa999b7ab410dcde957
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550181"
---
# <a name="wditlvnextdialogtoken"></a>WDI\_TLV\_次\_ダイアログ\_トークン


WDI\_TLV\_次\_ダイアログ\_トークンは、次のアクションのフレームで使用されるダイアログのトークンを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE1

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                           |
|-------|-------------------------------------------------------|
| UINT8 | 次のアクションのフレームで使用されるダイアログ トークンです。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN](https://msdn.microsoft.com/library/windows/hardware/dn925844)

 

 




