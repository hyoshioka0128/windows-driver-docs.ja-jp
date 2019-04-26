---
title: パイプラインのレンダリング
description: パイプラインのレンダリング
ms.assetid: 63672d6e-5c5d-4873-a104-991e0b17d128
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6245eb3154b6688c298a5a46dd1fa1e0d54d7d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350249"
---
# <a name="rendering-pipeline"></a>パイプラインのレンダリング


Direct3D のバージョン 10 をサポートするグラフィックス ハードウェアは、共有のプログラミング可能なシェーダーのコアを設計できます。 グラフィックス処理装置 (GPU) では、レンダリング パイプラインを構成する機能のブロックにわたってスケジュールできるシェーダー コアをプログラミングできます。 この負荷分散では、ハードウェア開発者が各シェーダーの種類がレンダリングを実行するために必要なものだけを使用する必要はないことを意味します。 この負荷分散できますしアクティブになっているシェーダーの種類のリソースを解放します。 次の図は、レンダリング パイプラインの機能ブロックを示しています。 図を次のセクションでは、さらに詳しくブロックについて説明します。

![レンダリング パイプラインの機能ブロックを示す図](images/pipeline.png)

### <a name="span-idinputassemblerspanspan-idinputassemblerspan-input-assembler"></a><span id="input_assembler"></span><span id="INPUT_ASSEMBLER"></span> 入力アセンブラー

[入力アセンブラー](input-assembler-stage.md)ステージでは、固定関数の動作を使用してメモリ不足の頂点を読み取ります。 入力アセンブラーは、フォームのジオメトリ プリミティブし、パイプラインに作業項目を作成します。 頂点の自動生成された識別子、インスタンス識別子 (頂点シェーダーに利用可能)、およびプリミティブ識別子 (ピクセル シェーダー、ジオメトリ シェーダーに利用可能) は、識別子に固有の処理を有効にします。 点線の図には、識別子に固有の処理の流れを示します。

### <a name="span-idvertexshaderspanspan-idvertexshaderspan-vertex-shader"></a><span id="vertex_shader"></span><span id="VERTEX_SHADER"></span> 頂点シェーダー

[頂点シェーダー](vertex-shader-stage.md)ステージ 1 つの頂点の入力として受け取り 1 つの頂点を出力します。

### <a name="span-idgeometryshaderspanspan-idgeometryshaderspan-geometry-shader"></a><span id="geometry_shader"></span><span id="GEOMETRY_SHADER"></span> ジオメトリ シェーダー

[ジオメトリ シェーダー](geometry-shader-stage.md)ステージは、入力として 1 つのプリミティブし、0、1、または複数のプリミティブを出力します。 出力のプリミティブは、ジオメトリ シェーダーをなくしてより多くのデータを含めることができます。 操作ごとの出力データの合計量は、(頂点数 x 頂点サイズ) です。

### <a name="span-idstreamoutputspanspan-idstreamoutputspan-stream-output"></a><span id="stream_output"></span><span id="STREAM_OUTPUT"></span> Stream の出力

[出力のストリーミング](stream-output-stage.md)ステージの出力バッファーにジオメトリ シェーダーの出力に到達 (ストリーム アウト) プリミティブを連結します。 ストリーム出力は、ジオメトリ シェーダーに関連付けと、まとめて両方プログラミングされます。

### <a name="span-idrasterizerspanspan-idrasterizerspan-rasterizer"></a><span id="rasterizer"></span><span id="RASTERIZER"></span> ラスタライザー

[ラスタライザー](rasterizer-block.md)クリップ (カスタムのクリップの境界を含む) のプリミティブをステージング、プリミティブのパースペクティブの除算を実行します、ビューポートとシザリングの選択を実装、レンダー ターゲットの選択を実行およびプリミティブのセットアップを実行します.

### <a name="span-idpixelshaderspanspan-idpixelshaderspan-pixel-shader"></a><span id="pixel_shader"></span><span id="PIXEL_SHADER"></span> ピクセル シェーダー

[ピクセル シェーダー](pixel-shader-stage.md)ステージは入力として 1 つのピクセルと同じ位置にある 1 つのピクセルまたはないピクセルを出力します。 ピクセル シェーダーは、現在のレンダー ターゲットを読み取ることができません。

### <a name="span-idoutputmergerspanspan-idoutputmergerspan-output-merger"></a><span id="output_merger"></span><span id="OUTPUT_MERGER"></span> 出力マージャー

[出力マージャー](output-merger-stage.md)ステージは、fixed 関数のレンダー ターゲットを実行します。 blend、深さ、テストとステンシル操作。

 

 





