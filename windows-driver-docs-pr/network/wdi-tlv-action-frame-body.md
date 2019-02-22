---
title: WDI_TLV_ACTION_FRAME_BODY
description: WDI_TLV_ACTION_FRAME_BODY では、アクションのフレームの本文を含む TLV です。
ms.assetid: 272782A9-F92E-4F32-A92B-B18EBE7C1803
ms.date: 07/18/2017
keywords:
- WDI_TLV_ACTION_FRAME_BODY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 561984937cf9fdda9f23d7368d4d25e744788a85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551813"
---
# <a name="wditlvactionframebody"></a>WDI\_TLV\_アクション\_フレーム\_本文


WDI\_TLV\_アクション\_フレーム\_本文は、アクションのフレームの本文を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xBE

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                           |
|-----------|-----------------------------------------------------------------------|
| UINT8\[\] | アクションのフレームの本文を含む UINT8 要素の配列。 |

 

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

 

 




