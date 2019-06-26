---
title: 7 番目の画像デコード構成
description: 7 番目の画像デコード構成
ms.assetid: eb52cdb4-4009-4860-80ac-5c2172f8a9b3
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
- WDK DirectX VA を設定する画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 568196b940beff4cf2cb704c12ae7aa9d0977c19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365519"
---
# <a name="seventh-picture-decoding-configuration"></a>7 番目の画像デコード構成


## <span id="ddk_seventh_picture_decoding_configuration_gg"></span><span id="DDK_SEVENTH_PICTURE_DECODING_CONFIGURATION_GG"></span>


このセットの 7 番目の構成がに対してのみ定義されている、 [MPEG2\_C](mpeg2-c.md)と[MPEG2\_D](mpeg2-d.md)に制限されているプロファイルが示されている、 [ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)構造体。 その他の制限プロファイルには、最小限の相互運用性セットにこの構成が含まれます。

(これは推奨される構成ではありません)、この構成でと同じ方法が定義されている、[構成をデコードする最初の画像](first-picture-decoding-configuration.md)次の例外。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>Zero</p></td>
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

 

 

 





