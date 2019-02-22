---
title: テクスチャの複数の検証
description: テクスチャの複数の検証
ms.assetid: 3f56f7c1-89d6-40d0-9540-b6280379ddc5
keywords:
- 複数のテクスチャ WDK Direct3D、検証
- テクスチャ管理 WDK Direct3D、検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629c742b29620f8670bc4974ad47107f8cb38bb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559552"
---
# <a name="multiple-texture-validation"></a>テクスチャの複数の検証


## <span id="ddk_multiple_texture_validation_gg"></span><span id="DDK_MULTIPLE_TEXTURE_VALIDATION_GG"></span>


現在のハードウェア実装されていません必ずしもすべての Direct3D が表すことができます。 アプリケーションでは、目的の描画モードを最初の設定と、呼び出し元によって、特定の描画操作を実行できるかどうかを決定、 **IDirect3DDevice7::ValidateDevice**メソッド。 ドライバーが初期化時およびサポートにその機能を正確に報告する必要があります[ **D3dValidateTextureStageState** ](https://msdn.microsoft.com/library/windows/hardware/ff549064)を検証するには、その機能を許可します。 検証では、TBLEND レベルで指定された操作についても説明します。 について**IDirect3DDevice7::ValidateDevice**、Direct3D SDK のドキュメントを参照してください。

次の表に、リターン コードを**IDirect3DDevice7::ValidateDevice**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONFLICTINGTEXTUREFILTER</p></td>
<td align="left"><p>Trilinear フィルタ リングと同時に複数のテクスチャ、ハードウェアを実行できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TOOMANYOPERATIONS</p></td>
<td align="left"><p>ハードウェアは、指定した数のオプションを処理できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDALPHAARG</p></td>
<td align="left"><p>指定したアルファ引数はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDALPHAOPERATION</p></td>
<td align="left"><p>指定されたアルファの操作はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDCOLORARG</p></td>
<td align="left"><p>指定した色の引数はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>指定した色の操作はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDFACTORVALUE</p></td>
<td align="left"><p>ハードウェアは 1.0 よりも大きい D3DTA_TFACTOR をサポートできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRONGTEXTUREFORMAT</p></td>
<td align="left"><p>ハードウェアは、選択したテクスチャ形式で現在の状態をサポートすることはできません。</p></td>
</tr>
</tbody>
</table>

 

 

 





