---
title: Direct3D シェーダーのコード
description: Direct3D シェーダーのコード
ms.assetid: 30d14bbe-10fe-46fc-99b3-ab2f989abb29
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d90b33671733db94651b20d5e15e38230111c572
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384868"
---
# <a name="direct3d-shader-codes"></a>Direct3D シェーダーのコード


ピクセル シェーダーのコードに依存して、D3DHAL\_コマンド ストリーム内で DP2CREATEPIXELSHADER 構造体。 DirectX 8.1 と以前では、頂点シェーダーのコードに依存して、D3DHAL\_DP2CREATEVERTEXSHADER 構造体。 DirectX 9.0 以降、頂点シェーダーのコードに依存して、D3DHAL\_DP2CREATEVERTEXSHADERFUNC 構造体。 ドライバーの D3dDrawPrimitives2 関数を呼び出すときに、ランタイムは、ピクセルまたは頂点シェーダーを作成します。 ピクセル シェーダーを作成するには、共通言語ランタイムは、D3DDP2OP で D3dDrawPrimitives2\_CREATEPIXELSHADER 操作コード。 頂点シェーダーを作成する DirectX 8.1 以降では、ランタイムが呼び出すと、D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADER 操作コード。 頂点シェーダーを作成する DirectX 9.0 以降では、ランタイムが呼び出すと、D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADERFUNC 操作コード。

このセクションには、個々 のシェーダー コードおよび各シェーダー コードを構成するトークンの形式について説明します。

[シェーダー コードの形式](shader-code-format.md)

[シェーダー コードのトークン](shader-code-tokens.md)

[シェーダーの操作コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)

[シェーダー レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)

[シェーダーの相対アドレス指定](shader-relative-addressing.md)

 

 





