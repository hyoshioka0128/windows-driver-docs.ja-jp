---
title: シェーダー コードの処理
description: シェーダー コードの処理
ms.assetid: c858766c-b414-4971-b4d9-23ec94aca8ea
keywords:
- ユーザーモード表示ドライバー WDK Windows Vista、シェーダーコード
- シェーダーコード WDK ディスプレイ
- ピクセルシェーダーコードの WDK ディスプレイ
- 頂点シェーダーコードの WDK ディスプレイ
- 頂点宣言の WDK ディスプレイ
- トークンの WDK 表示
- トークンの終了 WDK 表示
- WDK 表示の宣言
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b18df81c9763f1a3ec21a78f4d03cea60276435
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829685"
---
# <a name="processing-shader-codes"></a>シェーダー コードの処理


ユーザーモードの表示ドライバーは、頂点宣言と、各ピクセルと頂点シェーダーコード内のトークンを使用して、シェーダーアセンブラーをプログラミングします。

Microsoft Direct3D ランタイムがドライバーの[**CreateVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderfunc)関数と[**CreatePixelShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createpixelshader)関数を呼び出すと、ユーザーモードの表示ドライバーは、頂点とピクセルシェーダーコードを受け取ります。 ユーザーモードの表示ドライバーは、ランタイムがドライバーの[**CreateVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderdecl)関数を呼び出すと、頂点宣言を受け取ります。 頂点宣言は、 [**D3DDDIVERTEXELEMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddivertexelement)構造体の配列で構成されます。 ユーザーモードの表示ドライバーは、シェーダーコードと頂点シェーダーの宣言をハードウェア固有の形式に変換し、シェーダーのコードと宣言をシェーダーハンドルおよび宣言ハンドルに関連付けます。 ランタイムは、 [**SetVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderdecl)、 [**SetVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderfunc)、 [**SetPixelShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setpixelshader)の各関数の呼び出しで作成されたハンドルを使用して、後続のすべての描画を行うために頂点シェーダーの宣言と頂点とピクセルシェーダーを設定します。操作はこれらを使用します。

個々のシェーダーコードの形式と各シェーダーコードを構成するトークンの詳細については、「 [Direct3D シェーダー](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-shader-codes)コード」を参照してください。

アプリケーションで頂点シェーダー、ピクセルシェーダー、および頂点宣言を作成するときに、各のシェーダーコードと宣言が[終了トークン](https://docs.microsoft.com/windows-hardware/drivers/display/end-token)で終了する   に**注意**してください。 さらに、Direct3D ランタイムが頂点シェーダー作成要求をユーザーモードのディスプレイドライバーに渡し、要求に付随する頂点シェーダーとピクセルシェーダーのコードは終了トークンで終了します。 ただし、ランタイムが頂点宣言の作成要求を渡すとき、要求に付随する頂点宣言は終了トークンで終了しません。

 

 

 





