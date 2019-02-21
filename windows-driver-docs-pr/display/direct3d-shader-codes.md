---
title: Direct3D のシェーダー コード
description: Direct3D のシェーダー コード
ms.assetid: 30d14bbe-10fe-46fc-99b3-ab2f989abb29
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4dfb86c7b4a6547116f4a4df2a8013b75448279f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559388"
---
# <a name="direct3d-shader-codes"></a>Direct3D のシェーダー コード


ピクセル シェーダーのコードに依存して、D3DHAL\_コマンド ストリーム内で DP2CREATEPIXELSHADER 構造体。 DirectX 8.1 と以前では、頂点シェーダーのコードに依存して、D3DHAL\_DP2CREATEVERTEXSHADER 構造体。 DirectX 9.0 以降、頂点シェーダーのコードに依存して、D3DHAL\_DP2CREATEVERTEXSHADERFUNC 構造体。 ドライバーの D3dDrawPrimitives2 関数を呼び出すときに、ランタイムは、ピクセルまたは頂点シェーダーを作成します。 ピクセル シェーダーを作成するには、共通言語ランタイムは、D3DDP2OP で D3dDrawPrimitives2\_CREATEPIXELSHADER 操作コード。 頂点シェーダーを作成する DirectX 8.1 以降では、ランタイムが呼び出すと、D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADER 操作コード。 頂点シェーダーを作成する DirectX 9.0 以降では、ランタイムが呼び出すと、D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADERFUNC 操作コード。

このセクションには、個々 のシェーダー コードおよび各シェーダー コードを構成するトークンの形式について説明します。

[シェーダー コードの形式](shader-code-format.md)

[シェーダー コードのトークン](shader-code-tokens.md)

[シェーダーの操作コード](https://msdn.microsoft.com/library/windows/hardware/ff569706)

[シェーダー レジスタの種類](https://msdn.microsoft.com/library/windows/hardware/ff569707)

[シェーダーの相対アドレス指定](shader-relative-addressing.md)

 

 





