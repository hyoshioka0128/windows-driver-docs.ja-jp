---
title: 複数テクスチャの検証
description: 複数テクスチャの検証
ms.assetid: 3f56f7c1-89d6-40d0-9540-b6280379ddc5
keywords:
- 複数のテクスチャ WDK Direct3D、検証
- テクスチャ管理 WDK Direct3D、検証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f65e196503f132a738859273f8c4456d1bd9043
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840536"
---
# <a name="multiple-texture-validation"></a>複数テクスチャの検証


## <span id="ddk_multiple_texture_validation_gg"></span><span id="DDK_MULTIPLE_TEXTURE_VALIDATION_GG"></span>


現在のハードウェアは、必ずしも Direct3D が表現できるすべてのものを実装するわけではありません。 アプリケーションは、最初に目的のブレンドモードを設定してから、 **IDirect3DDevice7:: ValidateDevice**メソッドを呼び出すことによって、特定のブレンド操作を実行できるかどうかを判断します。 ドライバーは初期化時にその機能を正確に報告する必要があり、機能の検証を可能にするために[**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)をサポートします。 検証では、TBLEND レベルで指定された操作についても説明します。 **IDirect3DDevice7:: ValidateDevice**の詳細については、Direct3D SDK のドキュメントを参照してください。

次の表は、 **IDirect3DDevice7:: ValidateDevice**のリターンコードを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONFLICTINGTEXTUREFILTER</p></td>
<td align="left"><p>このハードウェアでは、トライリニアフィルターと複数のテクスチャを同時に実行することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TOOMANYOPERATIONS</p></td>
<td align="left"><p>指定された数のオプションをハードウェアが処理できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDALPHAARG</p></td>
<td align="left"><p>指定されたアルファ引数はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDALPHAOPERATION</p></td>
<td align="left"><p>指定されたアルファ操作はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDCOLORARG</p></td>
<td align="left"><p>指定されたカラー引数はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>指定されたカラー操作はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDFACTORVALUE</p></td>
<td align="left"><p>ハードウェアは1.0 より大きい D3DTA_TFACTOR をサポートできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRONGTEXTUREFORMAT</p></td>
<td align="left"><p>ハードウェアは、選択されたテクスチャ形式の現在の状態をサポートできません。</p></td>
</tr>
</tbody>
</table>

 

 

 





