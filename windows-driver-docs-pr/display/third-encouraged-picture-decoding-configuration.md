---
title: 3 番目の推奨される画像デコード構成
description: 3 番目の推奨される画像デコード構成
ms.assetid: 9f905030-9fc9-4a5f-8cf5-a36c7861be52
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
- WDK DirectX VA を設定する画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e5c5ed5e55cc7efd9f3e86c4cf1fbce0bce12a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389886"
---
# <a name="third-encouraged-picture-decoding-configuration"></a>3 番目の推奨される画像デコード構成


## <span id="ddk_third_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_THIRD_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


3 番目の推奨構成では、一部の実装で予想されるオフホスト IDCT のサポートを提供します。 この構成は、デコーダーのことをお勧めします。 ただし、2 つ目の構成は、アクセラレータを勧めします。

この構成でと同じ方法が定義されている、[構成をデコードする最初の画像](first-picture-decoding-configuration.md)次の例外。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfig4GroupedCoefs</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





