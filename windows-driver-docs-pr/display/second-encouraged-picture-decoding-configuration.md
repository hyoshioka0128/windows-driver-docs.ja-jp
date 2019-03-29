---
title: 2 番目の推奨される画像デコード構成
description: 2 番目の推奨される画像デコード構成
ms.assetid: 9e259768-4588-4a5b-b01b-fca0021cd966
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
- WDK DirectX VA を設定する画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c8941d02cbc311a0a801df7f972143d610e954e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582261"
---
# <a name="second-encouraged-picture-decoding-configuration"></a>2 番目の推奨される画像デコード構成


## <span id="ddk_second_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_SECOND_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


2 つ目の推奨構成では、オフホスト IDCT アクセラレータのサポートの強化を提供します。 このセットの最初の構成を実装するアクセラレータには、2 つ目をサポートする必要があります。 両方の構成のサポートを実装するのでは、アクセラレータ機能を使用できるように柔軟です。

この構成でと同じ方法が定義されている、[構成をデコードする最初の画像](first-picture-decoding-configuration.md)次の例外。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">[値]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigHostInverseScan</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





