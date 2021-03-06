---
title: 頂点ストリーム頻度の変更
description: 頂点ストリーム頻度の変更
ms.assetid: 81bbced4-7331-4e54-9617-1ef29b02f162
keywords:
- 頂点ストリーム頻度除算 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d381cb0c5a0cedc78fcc61e2b1c793c55af721
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385588"
---
# <a name="modifying-vertex-stream-frequency"></a>頂点ストリーム頻度の変更


## <span id="ddk_modifying_vertex_stream_frequency_gg"></span><span id="DDK_MODIFYING_VERTEX_STREAM_FREQUENCY_GG"></span>


頂点シェーダーのバージョン 3.0 以降をサポートするデバイスの DirectX 9.0 バージョンのドライバーでは、頂点ストリーム頻度除算を実装する必要があります。 バージョン 2.0 と頂点シェーダーが (fixed 関数を含む) の以前のモデルでは、頂点シェーダーが 1 回呼び出されます。 頂点ごと呼び出しごとに入力頂点レジスタは、頂点のストリームから要素を一意の頂点で初期化されます。 ただし、頂点ストリーム頻度除算を使用して、頂点シェーダー (3.0 以降) 呼び出せる頻度が低いレートで該当する入力のレジスタを初期化します。

アプリケーションを呼び出すと、 **IDirect3DDevice9::SetStreamSourceFreq**さらに、DirectX 9.0 ランタイムを指定したストリーム用の頻度を設定するメソッドを呼び出し、ドライバーの[ **D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 、D3DDP2OP を使用して機能\_SETSTREAMSOURCEFREQ 操作コード。

ストリームの周波数後除数 - たとえば、2 に設定されて、し、ドライバーが、ストリームからデータをフェッチし、すべて 2 つの頂点に適用可能な入力頂点レジスタにこのデータを渡す必要があります。 除数としてでは、ストリーム内の各要素に影響します。

ドライバーでは、この除数を使用して、次の数式に従って頂点バッファーに頂点のオフセットを計算します。

```cpp
VertexOffset = VertexIndex / Divider * StreamStride + StreamOffset 
```

ドライバーがドライバーの呼び出し中に頂点の開始値を受け取る場合に使用される、各頂点ストリーム*D3dDrawPrimitives2* 、D3DDP2OP を使用して機能\_DRAWPRIMITIVE オペレーション コード、ドライバーにもこの分割頻度除数で頂点の開始値との数式の結果。 この頂点の開始値で提供されます、 **VStart**のメンバー、 [ **D3DHAL\_DP2DRAWPRIMITIVE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2drawprimitive)構造体。 次の数式は、頂点の開始値で要因します。

```cpp
VertexOffset = StartVertex / Divider + 
               VertexIndex / Divider * StreamStride + StreamOffset 
```

この式が整数の除算を使用することに注意してください。

アプリケーションに渡す、D3DSBT\_VERTEXSTATE 状態の種類への呼び出しで、 **IDirect3DDevice9::CreateStateBlock**頂点の現在の状態をキャプチャするメソッド。

ドライバーでは、インデックス付きのプリミティブまたはドライバーがのみ version 3.0 (固定関数を含む) より前である頂点シェーダー モデルをサポートしているかどうかに、ストリームの頻度除数の設定は無視されます。

詳細については**IDirect3DDevice*Xxx*:: SetStreamSourceFreq**と**IDirect3DDevice*Xxx*:: CreateStateBlock**、最新の DirectX SDK ドキュメントを参照してください。

 

 





