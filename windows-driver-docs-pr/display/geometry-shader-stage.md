---
title: ジオメトリ シェーダー ステージ
description: ジオメトリ シェーダー ステージ
ms.assetid: 390eb917-3289-4b6e-be23-8db24cdd2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 066a47fbea947df7700cbd1990f714f30d032d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379982"
---
# <a name="geometry-shader-stage"></a>ジオメトリ シェーダー ステージ


ジオメトリ シェーダー (GS) のステージでは、入力と出力の頂点を生成することができますの頂点を持つアプリケーションで指定されたシェーダー コードを実行します。 頂点シェーダーは、1 つの頂点を操作とは異なり、ジオメトリ シェーダーの入力がさらに、端が隣接する頂点データ (つまり、線、三角形の 3 つの頂点またはポイントの 1 つの頂点の 2 つ頂点) の完全なプリミティブの頂点はプリミティブ (つまり、その他 2 つの頂点行) または三角形に 3 つの頂点。 次の図は、ジオメトリ シェーダーに渡される入力プリミティブの例を示します。

![ジオメトリ シェーダー プリミティブを示す図します。](images/geoshade.png)

ジオメトリ シェーダーへの別の入力は、入力アセンブラー (IA) によって自動生成されるプリミティブの ID です。 プリミティブの ID は、顔ごとのデータを必要な場合にフェッチまたはコンピューティング、ジオメトリ シェーダーを使用できます。

ジオメトリ シェーダーのステージでは、1 つ選択したトポロジを形成する複数の頂点を出力できます。 有効な GS 出力トポロジは*tristrip*、 *linestrip*、および*pointlist*します。 ジオメトリ シェーダーを作成できれば頂点の最大数を静的に宣言する必要がありますが、ジオメトリ シェーダーの出力のプリミティブの数、によって異なります。 ジオメトリ シェーダーを出力するストリップの長さは任意 (がある、**切り取り**コマンド)。

ラスタライザーをメモリ内の頂点バッファー、ジオメトリ シェーダーの出力を送信できます。 個々 のポイントの行にメモリに送信される出力が展開され、三角形は、(同様に出力がラスタライザーに渡される方法) を一覧表示されます。

ジオメトリ シェーダーのステージでは、次のアルゴリズムを実装できます。

-   ポイントのスプライト テセレーション:シェーダーは、1 つの頂点にし、任意のテクスチャ、normals、およびその他の属性を含んだ四角形の 4 つの角を表す 4 つの頂点 (2 つの出力の三角形) を生成します。

-   太線テセレーション:シェーダーは、2 つの行の頂点 (LV0 および LV1) を受信し、拡張の線を表す四角形の 4 つの頂点を生成します。 さらに、ジオメトリ シェーダーは、線の端点で mitering を実行するのに隣接する行の頂点 (AV0 および AV1) を使用できます。

-   ファー/Fin 生成。後ろの parallactic 効果をシミュレートするために異なるテクスチャ (押し出された面) で可能性のある複数のオフセットを表示します。 フィンは、角度の傾斜がない場合は多くの場合をフェードアウトするエッジが押し出されたです。 フィンは、斜体の角度に良く見えるオブジェクトの作成に使用されます。

-   ボリューム シャドウの生成:面を浮き出し表示するかどうかを判断するために使用する隣接情報です。

-   複数のテクスチャ キューブ面に単一パスの表示:プリミティブが射影され、ピクセル シェーダーの 6 回生成されます。 キューブの面を選択します。 レンダー ターゲット配列のインデックスでは、各プリミティブを伴います。

-   ピクセル シェーダーは、カスタム属性の補間を実行できるようにプリミティブ データとして重心座標を設定します。

-   異常のケース:アプリケーションでは、そのジオメトリ、n 更新プログラムでは、いくつかのジオメトリを生成し、し、そのジオメトリからシャドウ ボリュームを押し出しします。 このような場合は、マルチパスは頂点とプリミティブ データをストリーム出力し、データをバックアップする機能をソリューションです。

**注**  ジオメトリ シェーダーの各呼び出しが、さまざまな数の出力を生成するためのハードウェアに並列呼び出しはより難しくなりますこの段階で (頂点またはピクセル シェーダーのステージ) などでとステージの他のパイプラインの実行よりも並列です。 ジオメトリ シェーダーが呼び出しをアプリケーションでは、ジオメトリ シェーダーに達成可能な並列処理のレベルは必要ありません並列ジオメトリ シェーダーの呼び出し方法を実現するために必要な複雑なバッファリング、並列ハードウェアの実装が動作しています。ステージをするその他のパイプラインのステージと同様です。 つまり、ジオメトリ シェーダー、ジオメトリ シェーダーのあるプログラム負荷に応じてパイプラインでボトルネックになる可能性があります。 ただし、目的は、ジオメトリ シェーダーの機能を使用するアルゴリズムが、アプリケーションがプログラムでジオメトリを生成できないハードウェアで動作をエミュレートするよりも効率的に実行がまだです。

 

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ジオメトリ シェーダーを破棄します。

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**GsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**GsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**GsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**GsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





