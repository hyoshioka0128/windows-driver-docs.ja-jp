---
title: MPEG2_C
description: MPEG2_C
ms.assetid: 610ca80d-b29a-4c30-98df-8df8fe825157
keywords:
- MPEG2_C プロファイル WDK DirectX VA を制限します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efdd51cc9e0cc8fec615e36c1dce9534acac1b4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530730"
---
# <a name="mpeg2c"></a>MPEG2\_C


## <span id="ddk_mpeg2_c_gg"></span><span id="DDK_MPEG2_C_GG"></span>


MPEG2\_C の制限プロファイルには、mpeg-2 ビデオのメイン プロファイルをサポートするために必要な機能のセットが含まれています。 このプロファイルのサポートは、ビデオ アクセラレータ ドライバー ハードウェア ビデオ アクセラレータ機能を提供する必要があります。

MPEG2\_のアクセラレータの要件を緩和したトークンによって制限されている C プロファイルが定義されている、 [MPEG2\_A](mpeg2-a.md) (により、最小限のメンバーのいずれかをサポートしないようにアクセラレータ プロファイルMPEG2 の相互運用性の設定\_A)、MPEG2 をサポートするすべてのアクセラレータ\_プロファイルは、MPEG2 をサポートする必要があります\_C プロファイル。 同様に、すべてのアクセラレータをサポートする、 [MPEG2\_D](mpeg2-d.md)プロファイルは、MPEG2 をサポートする必要があります\_C プロファイル。

MPEC2 に対する制限\_MPEG2 用に示された制限によって C が定義されている\_A は、以下の制限を除く。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA に関する制限事項\_ConnectMode

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_C</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanrestrictions-on-dxvaconfigpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA に関する制限事項\_ConfigPictureDecode

このプロファイルに追加の構成を追加します、[最小限の相互運用性セット](minimal-interoperability-configuration-sets.md)の画像をデコードします。 この追加の構成は次の DXVA\_ConfigPictureDecode メンバー。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





