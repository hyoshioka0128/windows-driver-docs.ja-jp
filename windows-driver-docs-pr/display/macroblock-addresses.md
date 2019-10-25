---
title: マクロブロック アドレス
description: マクロブロック アドレス
ms.assetid: f04c5462-db7c-4917-b8ef-22a630c82994
keywords:
- マクロが WDK DirectX VA、アドレスをブロックする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e25691e4dd9255ba11ff8aba10d2f5acbc6bea1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840592"
---
# <a name="macroblock-addresses"></a>マクロブロック アドレス


## <span id="ddk_macroblock_addresses_gg"></span><span id="DDK_MACROBLOCK_ADDRESSES_GG"></span>


マクロブロックアドレスは、画像内のラスタースキャン順序におけるマクロブロックの位置です。 画像内のマクロブロックの水平方向と垂直位置は、指定された画像の幅と高さを使用して、マクロブロックアドレスから決定されます。これは、 **wPicWidthInMBminus1**メンバーと**wPicHeightInMBminus1**メンバーによって定義されます。[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体。 次に、マクロブロックアドレスの例をいくつか示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロブロック</th>
<th align="left">Address</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左上</p></td>
<td align="left"><p>回</p></td>
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

 

 

 





