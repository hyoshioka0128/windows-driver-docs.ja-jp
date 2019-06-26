---
title: 命令トークン
description: 命令トークン
ms.assetid: bfeee1ad-aaf3-41d0-a667-15d22eccd1e9
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4b373337d6f5d464fb4d6ced011c750a8d627450
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379896"
---
# <a name="instruction-token"></a>命令トークン


## <span id="ddk_instruction_token_gg"></span><span id="DDK_INSTRUCTION_TOKEN_GG"></span>


命令トークンでは、実行する特定の操作のドライバーに通知し、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_15_00_"></span> **\[15時 00分\]** ビット 0 ~ 15 を示し、[操作コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)します。 D3DSIO\_ \*操作コードの例は、場所\*命令を表します。 たとえば、次のコード例では、 [ADD 命令](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type):

```cpp
// D3DSIO_ADD d, s1, s2
```

<span id="_23_16_"></span> **\[23時 16分\]** ビット 16 ~ 23 が操作のコードに関連する特定のコントロールを示します。

<span id="_27_24_"></span> **\[27:24\]** ピクセルと頂点シェーダーより前のバージョン 2 の\_0、24 ~ 27 ビットで予約されている、0x0 に設定します。

ピクセルと頂点シェーダーのバージョン 2 の\_24 ~ 27 のビットが 0 以降では、命令トークン自体 (つまり、命令のトークンを含まない命令を構成するトークンの数) を含まない命令の Dword のサイズを指定します。

<span id="_28_"></span> **\[28\]** ピクセルと頂点シェーダーより前のバージョン 2 の\_0 ビット 28 は予約されている、0x0 に設定します。

ピクセルと頂点シェーダーのバージョン 2 の\_0 以降のビット 28 は、命令が基づいているかどうかを示します (つまり、シェーダー コードの最後に、余分な述語のソース トークンが含まれます。 このビットが 0x1 に設定されている場合、命令が実行されます。

<span id="_29_"></span> **\[29\]** 予約します。 この値は、「0x0」に設定されます。

<span id="_30_"></span> **\[30\]** ピクセル シェーダーのバージョン 2 よりも前の\_0、30 のビットがビット共同の問題。 場合 1 に設定されて、前の手順では、この命令の実行それ以外の場合、個別に実行します。

ピクセル シェーダーのバージョン 2 の\_0 およびそれ以降すべての頂点シェーダーのバージョンでは、30 ビットは予約されている、0x0 に設定します。

<span id="_31_"></span> **\[31\]**  31 のビットが 0 (0x0)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ビット 0 ~ 15 命令のトークンで指定できる操作の詳細については、最新の DirectX SDK ドキュメントでは、ピクセル シェーダーの参照と頂点シェーダーのリファレンスを参照してください。

DirectX3D ランタイムは、アプリケーションからシェーダー コードを受け取た後、ランタイムは、ドライバーのコードに渡す前に、コードを検証します。 ランタイム プレフィックスでアセンブリ命令の通常は、"D3DSIO\_"、操作コードを作成します。 たとえば、アセンブラーの次の手順では、カーネル モード操作に対応しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アセンブラー命令</th>
<th align="left">カーネル モード操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>add</strong></p></td>
<td align="left"><p>D3DSIO_ADD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mov</strong></p></td>
<td align="left"><p>D3DSIO_MOV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sub</strong></p></td>
<td align="left"><p>D3DSIO_SUB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>tex</strong></p></td>
<td align="left"><p>D3DSIO_TEX</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>texcoord</strong></p></td>
<td align="left"><p>D3DSIO_TEXCOORD</p></td>
</tr>
</tbody>
</table>

 

すべての頂点シェーダーのバージョンでは、注意してください、 **sub**アセンブラー命令は、D3DSIO として実装\_設定否定する 2 番目のソース (0x1) のソースの修飾子 (ビット 27:24) で追加の操作。

**Tex**と**テクスチャ座標**手順は、ピクセル シェーダーのバージョン 1 に適用されます\_0 ~ 1\_3; 各命令では、1 つ[destination パラメーター](destination-parameter-token.md)。関連付けられています。

**Texld**と**texcrd**手順については、ピクセル シェーダーのバージョン 1 に新しい\_4 以降それぞれの命令が両方の変換先および[パラメーターをソース](source-parameter-token.md)。関連付けられています。

ランタイムに変換します、 **tex**と**texld** 、D3DSIO アセンブラー指示\_TEX カーネル モードで動作します。 ランタイムに変換、**テクスチャ座標**と**texcrd**アセンブラー指示、D3DSIO\_テクスチャ座標のカーネル モード操作。 ドライバーは、シェーダー コードのピクセル シェーダーのバージョンをまず確認し、必要に応じて指示を処理します。 たとえば、ドライバーは、その受信 it バージョン 1 を確認します。\_4 ピクセル シェーダー コード、D3DSIO\_TEX 操作では、次の命令のトークンをコピー先とソース パラメーターにドライバーが決定します。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





