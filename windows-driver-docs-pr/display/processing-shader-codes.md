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
ms.openlocfilehash: 0c11a3fc9e7a3d2d91f4d6956dbb3b22026b6ee3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383912"
---
# <a name="processing-shader-codes"></a>シェーダー コードの処理


ユーザー モードでは、プログラムのシェーダー アセンブラーにドライバーは頂点の宣言、および各個々 のピクセルと頂点シェーダーのコード内でトークンを表示します。

マイクロソフトの Direct3D ランタイムが呼び出す、ドライバーのときに、ユーザー モードのディスプレイ ドライバーは頂点とピクセル シェーダーのコードを受信[ **CreateVertexShaderFunc** ](https://msdn.microsoft.com/library/windows/hardware/ff540717)と[ **CreatePixelShader** ](https://msdn.microsoft.com/library/windows/hardware/ff540668)関数、それぞれします。 ランタイムが呼び出す、ドライバーの場合、ユーザー モードのディスプレイ ドライバーが頂点宣言を受け取る[ **CreateVertexShaderDecl** ](https://msdn.microsoft.com/library/windows/hardware/ff540714)関数。 頂点宣言の配列から成る[ **D3DDDIVERTEXELEMENT** ](https://msdn.microsoft.com/library/windows/hardware/ff544344)構造体。 ユーザー モードのディスプレイ ドライバーは、シェーダー コードと頂点シェーダーの宣言をハードウェアに固有の書式に変換し、シェーダー コードおよび宣言シェーダーと宣言のハンドルに関連付けます。 ランタイムの呼び出しで作成されたハンドルを使用して、 [ **SetVertexShaderDecl**](https://msdn.microsoft.com/library/windows/hardware/ff569692)、 [ **SetVertexShaderFunc**](https://msdn.microsoft.com/library/windows/hardware/ff569693)、および[**SetPixelShader** ](https://msdn.microsoft.com/library/windows/hardware/ff569543)後続のすべての描画操作で使用できるように、宣言と頂点とピクセル シェーダー頂点シェーダーを設定する関数。

個々 のシェーダー コードと各シェーダー コードを構成するトークン形式の詳細については、次を参照してください。 [Direct3D のシェーダー コード](https://msdn.microsoft.com/library/windows/hardware/ff552891)します。

**注**  でシェーダー コードとそれぞれの宣言が終了アプリケーションでは、頂点シェーダー、ピクセル シェーダーおよび頂点宣言を作成するとき、[トークンの終了](https://msdn.microsoft.com/library/windows/hardware/ff564170)します。 終了トークンを使用したときに、Direct3D ランタイムがさらに、頂点を渡すし、ピクセル シェーダーの作成要求をユーザー モードには、要求に付属しているドライバー、頂点とピクセル シェーダーのコードを表示を終了します。 ただし、ランタイムは、作成要求を頂点宣言に渡す、ときに、要求に付随する頂点宣言で終わらない終了トークンです。

 

 

 





