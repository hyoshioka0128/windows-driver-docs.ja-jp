---
title: マクロ ブロックのアドレス
description: マクロ ブロックのアドレス
ms.assetid: f04c5462-db7c-4917-b8ef-22a630c82994
keywords:
- WDK DirectX va なので、マクロ ブロックをアドレスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e609bb2729ffb292677697735cd821b790681efc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559914"
---
# <a name="macroblock-addresses"></a>マクロ ブロックのアドレス


## <span id="ddk_macroblock_addresses_gg"></span><span id="DDK_MACROBLOCK_ADDRESSES_GG"></span>


マクロ ブロックのアドレスは、画像内で順序をラスター スキャンで、マクロ ブロックの位置です。 使用して、指定した幅と、画像の高さで定義されているマクロ ブロックのアドレスからの図に、マクロ ブロックの水平および垂直方向の位置が決定されます、 **wPicWidthInMBminus1**と**wPicHeightInMBminus1**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体。 マクロ ブロックのアドレスのいくつかの例を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ ブロック</th>
<th align="left">Address</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong> + 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p>(<strong>wPicHeightInMBminus1</strong> + 1) x (<strong>wPicWidthInMBminus1</strong> + 1) - 1</p></td>
</tr>
</tbody>
</table>

 

 

 





