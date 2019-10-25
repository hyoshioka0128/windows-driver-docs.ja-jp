---
title: 頂点ストリーム頻度の変更
description: 頂点ストリーム頻度の変更
ms.assetid: 81bbced4-7331-4e54-9617-1ef29b02f162
keywords:
- 頂点ストリームの周波数分割 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9cbd8e7ebbe455ca971559246bc4d839d6da50c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840560"
---
# <a name="modifying-vertex-stream-frequency"></a>頂点ストリーム頻度の変更


## <span id="ddk_modifying_vertex_stream_frequency_gg"></span><span id="DDK_MODIFYING_VERTEX_STREAM_FREQUENCY_GG"></span>


頂点シェーダーバージョン3.0 以降をサポートするデバイスの DirectX 9.0 バージョンドライバーは、頂点ストリームの周波数除算を実装する必要があります。 バージョン2.0 と、頂点シェーダーの以前のモデル (固定関数を含む) では、頂点シェーダーは頂点ごとに1回呼び出されます。各呼び出しに対して、入力頂点レジスタは、頂点ストリームから一意の頂点要素を使用して初期化されます。 ただし、頂点ストリームの周波数除算を使用すると、頂点シェーダー (3.0 以降) を呼び出して、適用可能な入力レジスタをより少ない頻度で初期化できます。

アプリケーションが**IDirect3DDevice9:: SetStreamSourceFreq**メソッドを呼び出して特定のストリームの頻度を設定すると、DirectX 9.0 ランタイムは\_D3DDP2OP を使用してドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数を呼び出します。SETSTREAMSOURCEFREQ 操作コード。

ストリームの frequency 除数 (たとえば、2) が設定された後、ドライバーはストリームからデータをフェッチし、2つの頂点ごとに、該当する入力頂点レジスタにこのデータを渡す必要があります。 この除数は、ストリーム内の各要素に影響します。

ドライバーは、この除数を使用して、次の式に従って頂点バッファーへの頂点オフセットを計算します。

```cpp
VertexOffset = VertexIndex / Divider * StreamStride + StreamOffset 
```

使用される各頂点ストリームについて、ドライバーが D3DDP2OP\_DRAWPRIMITIVE 操作コードを使用してドライバーの*D3dDrawPrimitives2*関数の呼び出し中に開始頂点の値を受け取ると、ドライバーはこの開始頂点の値をfrequency 除数は、数式の結果を要因とします。 この開始頂点値は、 [**D3DHAL\_DP2DRAWPRIMITIVE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2drawprimitive)構造体の**vstart**メンバーに指定されています。 次の式では、開始頂点の値が考慮されます。

```cpp
VertexOffset = StartVertex / Divider + 
               VertexIndex / Divider * StreamStride + StreamOffset 
```

上の数式では、整数除算が使用されていることに注意してください。

アプリケーションは、現在の頂点の状態をキャプチャするために、 **IDirect3DDevice9:: CreateStateBlock**メソッドの呼び出しで D3DSBT\_vertexstate の種類を渡します。

ドライバーは、インデックス付きプリミティブの場合、またはドライバーがバージョン 3.0 (固定関数を含む) より前の頂点シェーダーモデルのみをサポートしている場合に、ストリームの frequency 除数の設定を無視します。

**IDirect3DDevice*xxx*:: SetStreamSourceFreq**と**IDirect3DDevice*xxx*:: CreateStateBlock**の詳細については、最新の DirectX SDK のドキュメントを参照してください。

 

 





