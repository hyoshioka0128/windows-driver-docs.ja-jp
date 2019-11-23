---
title: ジオメトリ シェーダー ステージ
description: ジオメトリ シェーダー ステージ
ms.assetid: 390eb917-3289-4b6e-be23-8db24cdd2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1336682c1644ed9d5e7760c0bc8ade4970aa2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839682"
---
# <a name="geometry-shader-stage"></a>ジオメトリ シェーダー ステージ


ジオメトリシェーダー (GS) ステージは、アプリケーションで指定されたシェーダーコードを、頂点を入力として実行し、出力時に頂点を生成することができます。 1つの頂点で動作する頂点シェーダーとは異なり、ジオメトリシェーダーの入力は、完全なプリミティブの頂点 (つまり、直線の場合は2つの頂点、三角形の場合は3頂点、ポイントの場合は1頂点) とエッジ隣接の頂点データを持ちます。プリミティブ (直線の場合は2つの頂点、三角形の場合は追加の3つの頂点)。 次の図は、ジオメトリシェーダーへの入力であるプリミティブの例を示しています。

![ジオメトリシェーダープリミティブを示す図](images/geoshade.png)

ジオメトリシェーダーへのもう1つの入力は、入力アセンブラ (IA) によって自動生成されるプリミティブ ID です。 プリミティブ ID を使用すると、必要に応じて表面データをフェッチまたは計算できます。

ジオメトリシェーダーステージは、1つの選択されたトポロジを形成するために複数の頂点を出力できます。 使用可能な GS 出力トポロジは、 *tristrip*、 *linestrip*、および*pointlist*です。 ジオメトリシェーダーによって出力されるプリミティブの数は変化しますが、ジオメトリシェーダーが生成できる頂点の最大数は静的に宣言する必要があります。 ジオメトリシェーダーが出力するストリップの長さは任意です ( **cut**コマンドがあります)。

ジオメトリシェーダーの出力は、ラスタライザーおよびメモリ内の頂点バッファーに送信できます。 メモリに送信される出力は、個々のポイント、線、および三角形のリストに展開されます (出力がラスタライザーに渡される方法と同様です)。

ジオメトリシェーダーステージは、次のアルゴリズムを実装できます。

-   ポイントスプライトテセレーション: シェーダーは、1つの頂点を受け取り、任意の texcoords、法線、およびその他の属性を持つ4つの頂点 (2 つの出力三角形) を生成します。

-   ワイドラインテセレーション: シェーダーは2つの直線頂点 (LV0 と LV1) を受け取り、拡大された直線を表す4つの頂点を4つ生成します。 さらに、ジオメトリシェーダーでは、隣接する行頂点 (AV0 および AV1) を使用して、mitering 上の行エンドポイントを実行できます。

-   一番/Fin 生成: 異なるテクスチャ (押し出し faces) で複数のオフセットをレンダリングして、一番の parallactic 効果をシミュレートします。 フィンは、角度が斜投影されていない場合にフェードアウトすることが多い、押し出しのエッジです。 フィンは、オブジェクトが斜めに見えるようにするために使用されます。

-   シャドウボリュームの生成: 押し出しを行うかどうかを決定するために使用される隣接情報。

-   複数のテクスチャキューブの面へのシングルパスレンダリング: プリミティブが射影され、ピクセルシェーダーに6回出力されます。 各プリミティブには、キューブ面を選択するレンダーターゲットの配列インデックスが付属しています。

-   ピクセルシェーダーがカスタム属性補間を実行できるように、重心座標をプリミティブデータとして設定します。

-   Pathological の場合: アプリケーションによっていくつかのジオメトリが生成され、その後、ジオメトリを持つ n パッチが生成され、そのジオメトリからシャドウボリュームが押し出しされます。 このような場合、マルチパスは、頂点とプリミティブデータをストリームに出力して、データを元に戻す機能を備えたソリューションです。

**注**   ジオメトリシェーダーへの呼び出しごとに異なる数の出力が生成される可能性があるため、この段階では、他のパイプラインステージ (頂点シェーダーまたはピクセルシェーダーステージなど) を並列で実行する場合よりも、ハードウェアへの並列呼び出しの方が困難です。 ハードウェアの実装では、ジオメトリシェーダー呼び出しを並列で実行しますが、並列ジオメトリシェーダー呼び出しを実行するために必要な複雑なバッファリングは、アプリケーションで、ジオメトリシェーダーで実現可能な並列処理のレベルを必要としないことを意味します。ステージは、他のパイプラインステージと同じくらいになります。 つまり、ジオメトリシェーダーに含まれるプログラムの負荷に応じて、パイプラインのボトルネックになることがあります。 ただし、目標は、ジオメトリシェーダーの機能を使用するアルゴリズムは、プログラムによって geometry を生成できないハードウェアの動作をエミュレートする必要があるアプリケーションよりも効率的に実行されることです。

 

Direct3D ランタイムは、次のドライバー関数を呼び出して、ジオメトリシェーダーを作成、設定、および破棄します。

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**GsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**GsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**GsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**GsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





