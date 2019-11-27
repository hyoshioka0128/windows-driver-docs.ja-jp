---
title: 入力アセンブラー ステージ
description: 入力アセンブラー ステージ
ms.assetid: 8db6a2ab-8354-4690-8141-2cdd91c77d5c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd733f6aa8806d218bfd5624548e9352ebd62c65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840365"
---
# <a name="input-assembler-stage"></a>入力アセンブラー ステージ


入力アセンブラー (IA) は、1-D バッファーからソースジオメトリデータを取得することによって、レンダリングパイプラインに三角形、線、またはポイントを導入します。

頂点データは、複数のバッファーから取得でき、各バッファーから構造体の配列形式でアクセスできます。 各バッファーは個々の入力スロットにバインドされ、構造のストライドが与えられます。 すべてのバッファーでのデータのレイアウトは入力宣言によって指定され、各エントリによって*要素*が定義されます。 要素には、入力スロット、構造オフセット、データ型、およびターゲットレジスタ (パイプラインの最初のアクティブなシェーダー用) が含まれています。

頂点の特定のシーケンスは、バッファーからフェッチされたデータから構築されます。 データは、固定関数の状態とさまざまな*Draw\** () DDI 呼び出しの組み合わせによって転送されるトラバーサルでフェッチされます。 さまざまなプリミティブトポロジ (ポイントリスト、行リスト、トライアングルリスト、トライアングルストリップなど) を使用して、頂点データのシーケンスをプリミティブのシーケンスとして表すことができます。

頂点データは、次の2つの方法のいずれかで生成できます。 頂点データを生成する最初の方法は、*インデックスなし*のレンダリングです。これは、頂点データを格納するバッファーの順次走査です。 頂点データは、各バッファーバインドで開始オフセットから開始されます。 頂点データを生成する2番目の方法は、*インデックス付き*レンダリングです。これは、スカラー整数インデックスを含む1つのバッファーのシーケンシャル走査です。 インデックスは、開始オフセットでバッファーに生成されます。 各インデックスは、頂点データを格納するバッファーからデータをフェッチする場所を示します。 インデックス値は、参照するバッファーの特性に依存しません。 バッファーは、宣言によって記述されます。 インデックス付きでない、またはインデックス付きのレンダリングでは、それぞれ独自の方法で、頂点データをメモリ内にフェッチし、その結果を頂点とプリミティブにアセンブルするアドレスを生成します。

インスタンス化された geometry レンダリングが有効になるのは、インデックス付きレンダリングでもインデックス付きレンダリングでも、各頂点バッファー内の範囲 (インデックスなしのケース) またはインデックスバッファー (インデックス付きの場合) をループするためです。 バッファーバインドは、*インスタンスデータ*または*頂点データ*として識別できます。 この id では、インスタンス化されたレンダリングの実行中にバインドされたバッファーを使用する方法を指定します。 インデックス付きでない、またはインデックス付きレンダリングによって生成されるアドレスは、頂点データをフェッチするために使用されます。これは、ランタイムがインスタンス化されたレンダリングを実行するときのループの対象にもなります。 一方、インスタンスデータは、インスタンスごとに1つのステップと同じ頻度で (たとえば、インスタンス内の頂点の数が走査された後の1つのステップ)、常にバッファーごとのオフセットから順番に順次スキャンされます。 インスタンスデータのステップレートを選択して、インスタンスの頻度を部分的に調和させることもできます (つまり、他のすべてのインスタンス、3番目のインスタンスごとなど)。

IA のもう1つの特殊なケースは、ストリーム出力ステージが書き込んだバッファーを読み取ることができることです。 このようなシナリオでは、新しい種類の描画操作である[**Drawauto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)が有効になります。 *Drawauto*を使用すると、ストリーム出力バッファーに書き込まれる動的な出力を CPU 関与なしで再利用でき、実際に書き込まれたデータの量を確認できます。

IA は、バッファーから頂点データを生成するだけでなく、レンダリングパイプラインのシェーダーステージへの入力のために、VertexID、PrimitiveID、および InstanceID という3つのスカラーカウンター値を自動生成できます。

トライアングルストリップなどのストリップトポロジのインデックス付きレンダリングでは、1つの * 描画\*<em>() 呼び出し *</em>* で複数のストリップを描画するためのメカニズムが用意されています (つまり、ストリップをカットするための * 切り取りコマンド)。

Direct3D ランタイムは、次のドライバー関数を呼び出して、IA を作成、設定、および破棄します。

[**CalcPrivateElementLayoutSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateelementlayoutsize)

[**CreateElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createelementlayout)

[**DestroyElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyelementlayout)

[**IaSetIndexBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)

[**IaSetInputLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setinputlayout)

[**IaSetTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_settopology)

[**IaSetVertexBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setvertexbuffers)

 

 





