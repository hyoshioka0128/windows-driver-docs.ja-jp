---
title: MPEG2_D
description: MPEG2_D
ms.assetid: f5cb5e49-c64c-46d2-92bb-68db1d9c5d18
keywords:
- MPEG2_D プロファイル WDK DirectX VA を制限します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54578361f7883c035bf97bab3e315fe4ccfd0d25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345644"
---
# <a name="mpeg2d"></a>MPEG2\_D


## <span id="ddk_mpeg2_d_gg"></span><span id="DDK_MPEG2_D_GG"></span>


MPEG2\_D の制限プロファイルには、mpeg-2 ビデオのメイン プロファイルとバック エンド ハードウェア サブピクチャ ブレンドを使用して、関連付けられている DVD サブピクチャをサポートするために必要な機能のセットが含まれています。

MPEG2\_D の制限プロファイルのアクセラレータの要件を緩和したトークンは、 [MPEG2\_B](mpeg2-b.md)プロファイル (アクセラレータは必要ありません、最小限の相互運用性をサポートするにはMPEG2 の\_B)、MPEG2 をサポートするすべてのドライバー\_B プロファイルは、MPEG2 をサポートする必要があります\_D プロファイル。 MPEG2 に対する制限\_D が、MPEG2 用に示された制限によって定義されている\_B は、次の追加の制限を除いて、プロファイルを制限します。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA に関する制限事項\_ConnectMode

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_D</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanrestrictions-on-dxvaconfigpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA に関する制限事項\_ConfigPictureDecode

これらの制限は、追加の構成を追加、[最小限の相互運用性のセット](minimal-interoperability-configuration-sets.md)画像のデコード (bDXVA\_Func を 1 に等しい)。 この追加の構成は次の DXVA\_ConfigPictureDecode メンバー。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">値</th>
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
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphacombinespanrestrictions-on-dxvaconfigalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHACOMBINE"></span>DXVA に関する制限事項\_ConfigAlphaCombine

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigBlendType</strong></p></td>
<td align="left"><p>0 または 1 (アクセラレータの裁量)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigalphaloadspanspan-idrestrictionsondxvaconfigalphaloadspanspan-idrestrictionsondxvaconfigalphaloadspanrestrictions-on-dxvaconfigalphaload"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad"></span><span id="restrictions_on_dxva_configalphaload"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD"></span>DXVA に関する制限事項\_ConfigAlphaLoad

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigDataType</strong></p></td>
<td align="left"><p>任意の値 (アクセラレータの裁量)。</p></td>
</tr>
</tbody>
</table>

 

 

 





