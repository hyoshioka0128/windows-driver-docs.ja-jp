---
title: 命令トークン
description: 命令トークン
ms.assetid: bfeee1ad-aaf3-41d0-a667-15d22eccd1e9
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 393880afbe3766137b20310471ae4fc731e78b8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840357"
---
# <a name="instruction-token"></a>命令トークン


## <span id="ddk_instruction_token_gg"></span><span id="DDK_INSTRUCTION_TOKEN_GG"></span>


命令トークンは、実行する特定の操作をドライバーに通知し、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>列

<span id="_15_00_"></span> **\[15:00\]** ビット 0 ~ 15 は[操作コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)を示します。 D3DSIO\_\* は、\* が命令を表す操作コードの例です。 たとえば、次のコードスニペットは[ADD 命令](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)を示しています。

```cpp
// D3DSIO_ADD d, s1, s2
```

<span id="_23_16_"></span> **\[23:16\]** ビット 16 ~ 23 は、操作コードに関連する特定のコントロールを示します。

<span id="_27_24_"></span> **\[27:24\]** 2\_0 より前のピクセルおよび頂点シェーダーバージョンでは、ビット 24 ~ 27 が予約され、0x0 に設定されます。

ピクセルおよび頂点シェーダーのバージョン 2\_0 以降の場合、ビット 24 ~ 27 は命令トークン自体 (つまり、命令トークンを除く命令を構成するトークンの数) を除く、命令の Dword のサイズを指定します。

<span id="_28_"></span> **\[28\]** 2\_0 より前のピクセルおよび頂点シェーダーバージョンでは、ビット28が予約され、0x0 に設定されます。

ピクセルおよび頂点シェーダーバージョン 2\_0 以降の場合、ビット28は命令が使用されるかどうかを示します (つまり、シェーダーコードの末尾に追加の述語ソーストークンが含まれます)。 このビットが0x1 に設定されている場合、命令は「」のようになります。

<span id="_29_"></span> **\[29\]** 確保. この値は0x0 に設定されます。

<span id="_30_"></span> **\[30\]** 2\_0 より前のピクセルシェーダーバージョンの場合、ビット30は共同問題のビットです。 1に設定した場合は、前の手順でこの命令を実行します。それ以外の場合は、個別に実行します。

ピクセルシェーダーバージョン 2\_0 以降のすべての頂点シェーダーバージョンでは、ビット30は予約され、0x0 に設定されます。

<span id="_31_"></span> **\[31\]** ビット31はゼロ (0x0) です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

ビット 0 ~ 15 の命令トークンで指定できる操作の詳細については、最新の DirectX SDK ドキュメントの「ピクセルシェーダーの参照と頂点シェーダーのリファレンス」を参照してください。

DirectX3D ランタイムは、アプリケーションからシェーダーコードを受け取ると、コードをドライバーに渡す前に、ランタイムがコードを検証します。 通常、ランタイムはアセンブラー命令を "D3DSIO\_" にプレフィックスとして操作コードを作成します。 たとえば、次のアセンブラ命令は、カーネルモードの操作に対応しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アセンブラー命令</th>
<th align="left">カーネルモードの操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>アドイン</strong></p></td>
<td align="left"><p>D3DSIO_ADD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mov</strong></p></td>
<td align="left"><p>D3DSIO_MOV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>サブ</strong></p></td>
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

 

すべての頂点シェーダーのバージョンでは、**サブ**アセンブラー命令は D3DSIO\_ADD 操作として実装され、2番目のソース修飾子 (ビット 27:24) が反転 (0x1) に設定されることに注意してください。

**Tex**および**texcoord**命令は、ピクセルシェーダーバージョン 1\_0 ~ 1\_3; に適用されます。各命令には、1つの[宛先パラメーター](destination-parameter-token.md)が関連付けられています。

**Texld**と**texld**の手順は、ピクセルシェーダーバージョン 1\_4 以降で新しく追加されました。各命令には、destination と source の両方の[パラメーター](source-parameter-token.md)が関連付けられています。

このランタイムは、 **tex**および**texld**アセンブラー命令を D3DSIO\_tex カーネルモードの操作に変換します。 ランタイムは、 **texcoord** **アセンブラー命令を D3DSIO**\_texcoord カーネルモードの操作に変換します。 ドライバーはまず、シェーダーコードのピクセルシェーダーバージョンを確認し、それに応じて指示を処理します。 たとえば、ドライバーがバージョン 1\_4 ピクセルシェーダーコードを受信したことを、D3DSIO\_の TEX 操作で確認した場合、ドライバーは destination および source パラメーターが命令トークンに従っていると判断します。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





