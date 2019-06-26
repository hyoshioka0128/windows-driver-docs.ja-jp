---
title: シェーダー コードの処理
description: シェーダー コードの処理
ms.assetid: c858766c-b414-4971-b4d9-23ec94aca8ea
keywords:
- ユーザー モード ドライバー WDK Windows Vista では、シェーダー コードの表示します。
- シェーダー コードの WDK の表示
- ピクセル シェーダー コードの WDK の表示
- 頂点シェーダー コードの WDK の表示
- 頂点宣言 WDK を表示します。
- トークンの WDK の表示
- 最後のトークンの WDK の表示
- WDK の宣言を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a80ce97f20035781860b4b62d82958a672a0a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363713"
---
# <a name="processing-shader-codes"></a>シェーダー コードの処理


ユーザー モードでは、プログラムのシェーダー アセンブラーにドライバーは頂点の宣言、および各個々 のピクセルと頂点シェーダーのコード内でトークンを表示します。

マイクロソフトの Direct3D ランタイムが呼び出す、ドライバーのときに、ユーザー モードのディスプレイ ドライバーは頂点とピクセル シェーダーのコードを受信[ **CreateVertexShaderFunc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderfunc)と[ **CreatePixelShader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createpixelshader)関数、それぞれします。 ランタイムが呼び出す、ドライバーの場合、ユーザー モードのディスプレイ ドライバーが頂点宣言を受け取る[ **CreateVertexShaderDecl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderdecl)関数。 頂点宣言の配列から成る[ **D3DDDIVERTEXELEMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddivertexelement)構造体。 ユーザー モードのディスプレイ ドライバーは、シェーダー コードと頂点シェーダーの宣言をハードウェアに固有の書式に変換し、シェーダー コードおよび宣言シェーダーと宣言のハンドルに関連付けます。 ランタイムの呼び出しで作成されたハンドルを使用して、 [ **SetVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderdecl)、 [ **SetVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderfunc)、および[**SetPixelShader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setpixelshader)後続のすべての描画操作で使用できるように、宣言と頂点とピクセル シェーダー頂点シェーダーを設定する関数。

個々 のシェーダー コードと各シェーダー コードを構成するトークン形式の詳細については、次を参照してください。 [Direct3D のシェーダー コード](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-shader-codes)します。

**注**  でシェーダー コードとそれぞれの宣言が終了アプリケーションでは、頂点シェーダー、ピクセル シェーダーおよび頂点宣言を作成するとき、[トークンの終了](https://docs.microsoft.com/windows-hardware/drivers/display/end-token)します。 終了トークンを使用したときに、Direct3D ランタイムがさらに、頂点を渡すし、ピクセル シェーダーの作成要求をユーザー モードには、要求に付属しているドライバー、頂点とピクセル シェーダーのコードを表示を終了します。 ただし、ランタイムは、作成要求を頂点宣言に渡す、ときに、要求に付随する頂点宣言で終わらない終了トークンです。

 

 

 





