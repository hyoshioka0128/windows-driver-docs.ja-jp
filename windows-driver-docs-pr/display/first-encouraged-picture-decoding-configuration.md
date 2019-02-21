---
title: 最初のことをお勧めの画像をデコード構成
description: 最初のことをお勧めの画像をデコード構成
ms.assetid: ad1c20a6-e070-4df0-91cd-6c2bd728e311
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
- WDK DirectX VA を設定する画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e181226cec6a2ace87fd2038a7da468c54b4ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558499"
---
# <a name="first-encouraged-picture-decoding-configuration"></a>最初のことをお勧めの画像をデコード構成


## <span id="ddk_first_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_FIRST_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


最初の推奨構成は、オフホスト ビット ストリームを高速化の処理のサポートの強化です。

この構成でと同じ方法が定義されている、[構成をデコードする最初の画像](first-picture-decoding-configuration.md)次の例外。

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
<td align="left"><p><strong>bConfigBitstreamRaw</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

 

 





