---
title: Direct3D シェーダーのコード
description: Direct3D シェーダーのコード
ms.assetid: 30d14bbe-10fe-46fc-99b3-ab2f989abb29
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c04e6c11064fd6b4d8cbfd5461624b54cbc6b390
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839005"
---
# <a name="direct3d-shader-codes"></a>Direct3D シェーダーのコード


ピクセルシェーダーコードは、コマンドストリームの D3DHAL\_DP2CREATEPIXELSHADER 構造体に従います。 DirectX 8.1 以前の場合、頂点シェーダーコードは D3DHAL\_DP2CREATEVERTEXSHADER 構造体に従います。 DirectX 9.0 以降では、頂点シェーダーコードは D3DHAL\_DP2CREATEVERTEXSHADERFUNC 構造体に従います。 ランタイムは、ドライバーの D3dDrawPrimitives2 関数を呼び出すときに、ピクセルシェーダーまたは頂点シェーダーを作成します。 ピクセルシェーダーを作成するために、ランタイムは D3DDP2OP\_CREATEPIXELSHADER 操作コードを使用して D3dDrawPrimitives2 を呼び出します。 DirectX 8.1 以前で頂点シェーダーを作成するために、ランタイムは、D3DDP2OP\_CREATEVERTEXSHADER 操作コードを使用して D3dDrawPrimitives2 を呼び出します。 DirectX 9.0 以降で頂点シェーダーを作成するために、ランタイムは D3DDP2OP\_CREATEVERTEXSHADERFUNC 操作コードを使用して D3dDrawPrimitives2 を呼び出します。

このセクションでは、個々のシェーダーコードの形式と、各シェーダーコードを構成するトークンについて説明します。

[シェーダーのコード形式](shader-code-format.md)

[シェーダーのコードトークン](shader-code-tokens.md)

[シェーダー操作コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)

[シェーダーレジスタの型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)

[シェーダーの相対アドレス指定](shader-relative-addressing.md)

 

 





