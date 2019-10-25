---
title: 7 番目の画像デコード構成
description: 7 番目の画像デコード構成
ms.assetid: eb52cdb4-4009-4860-80ac-5c2172f8a9b3
keywords:
- 圧縮された画像デコードセット WDK DirectX VA
- 画像デコードセット WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75562285ee5566f8c6de178beadfdec7ecaea8c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825732"
---
# <a name="seventh-picture-decoding-configuration"></a>7 番目の画像デコード構成


## <span id="ddk_seventh_picture_decoding_configuration_gg"></span><span id="DDK_SEVENTH_PICTURE_DECODING_CONFIGURATION_GG"></span>


このセットの7番目の構成は、 [**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)構造体に示されている[mpeg2\_C](mpeg2-c.md)および[mpeg2\_D](mpeg2-d.md)制限プロファイルに対してのみ定義されます。 その他の制限されたプロファイルには、最小相互運用性セットにこの構成が含まれていません。

この構成 (推奨される構成ではありません) は、最初の[画像デコード構成](first-picture-decoding-configuration.md)と同じように定義されています。ただし、次の例外があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfig4GroupedCoefs</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





