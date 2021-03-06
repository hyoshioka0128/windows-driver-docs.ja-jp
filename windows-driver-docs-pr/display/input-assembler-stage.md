---
title: 入力アセンブラー ステージ
description: 入力アセンブラー ステージ
ms.assetid: 8db6a2ab-8354-4690-8141-2cdd91c77d5c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8fbd37c2116f7225e1f562a9de1c888494a68c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385175"
---
# <a name="input-assembler-stage"></a>入力アセンブラー ステージ


入力アセンブラー (IA) は三角形、線、またはポイントをソース 1 D バッファーからの geometry 型のデータをプルして、レンダリング パイプラインに導入します。

頂点データは、複数のバッファーに由来して、各バッファーから、構造体への配列の形式でアクセスできます。 バッファーは各個々 の入力のスロットにバインドされているし、構造体のストライドを指定します。 すべてのバッファー間のデータのレイアウトが、入力宣言、各エントリを定義で指定された、*要素*します。 要素には、(パイプラインの最初のアクティブなシェーダー) 用の入力のスロット、構造体のオフセット、データ型、およびターゲットの登録が含まれています。

バッファーから取り出されているデータからの特定の頂点のシーケンスが構築されます。 固定機能の状態とさまざまな組み合わせによって、データがフェッチが指定されたトラバーサルで*描画\** DDI 呼び出し。 さまざまなプリミティブのトポロジ (たとえば、ポイントの一覧、行のリスト、三角形の一覧および三角形ストリップ)、一連のプリミティブの頂点データのシーケンスを利用できます。

頂点データは、2 つの方法のいずれかで生成されることができます。 頂点データを生成するために最初の方法は*インデックスのない*レンダリングでは、頂点データを含んでいるバッファーのシーケンシャル トラバーサルであります。 頂点データは、開始オフセットはバッファーの各バインディングで発生します。 頂点データを生成するために 2 つ目の方法は、*インデックス*レンダリングでは、スカラーの整数インデックスを含む 1 つのバッファーのトラバーサルがシーケンシャルであります。 インデックスは、バッファーには、開始オフセットで生成されたものです。 各インデックスでは、頂点データを格納しているバッファーからデータをフェッチする場所を示します。 インデックス値は、参照されているバッファーの特性に依存しません。 バッファーは宣言によって記述されます。 インデックス付きでないと、インデックス付き表示、それぞれに独自の方法で、メモリ内の頂点のデータをフェッチする元のアドレスを生成および頂点とプリミティブに、その後、結果をアセンブルします。

インスタンス化されたジオメトリのレンダリングは、各頂点バッファー (インデックス付きでない場合) 内の範囲のループまたはバッファー (インデックス付きの場合) のインデックス、非インデックスまたはインデックス付きのレンダリングで順次のトラバーサルを許可することで有効です。 バッファー バインディングとして識別できる*インスタンス データ*または*頂点データ*します。 この id は、インスタンス化されたレンダリングを実行中にバインドされたバッファーを使用する方法を指定します。 によって生成されるアドレス以外のインデックスを作成または頂点データは、ループ、ランタイムがインスタンス化されたレンダリングを実行するときにもアカウントをフェッチするインデックス付きのレンダリングが使われます。 インスタンス データをその一方が常に順番に通過インスタンス (たとえばは手順インスタンス内の頂点の数が走査転送後の 1 つ) ごとに 1 つの手順と同じ頻度でのバッファー オフセット位置から開始します。 手順レート インスタンスのデータは、インスタンス数 (つまり、1 つ一歩前進インスタンス、すべての 3 番目のインスタンスとその他のすべての) のサブ調和するも選択できます。

IA のもう 1 つの特殊なケースに書き込まれたバッファー ストリーム ステージの出力を読み取ることができます。 このようなシナリオにより、新しい種類の描画操作では、 [ **DrawAuto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)します。 *DrawAuto* CPU 操作で、データの量が実際に書き込まれたかを判断することがなく、再利用されるストリーム出力バッファーに書き込まれた出力の動的な量を許可します。

バッファーから頂点データを生成するには、だけでなく、IA できます自動生成 3 つのスカラーのカウンター値。VertexID、PrimitiveID、および InstanceID、レンダリング パイプラインのシェーダーのステージを入力します。

ストリップのトポロジ、三角形ストリップなどのインデックス付きのレンダリングを 1 つの複数のストリップを描画するためのメカニズムを提供 * 描画\*<em>() 呼び出し (つまり、**切り取り</em>* 切り取りコマンドストリップ)。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、IA を破棄します。

[**CalcPrivateElementLayoutSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateelementlayoutsize)

[**CreateElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createelementlayout)

[**DestroyElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyelementlayout)

[**IaSetIndexBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)

[**IaSetInputLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setinputlayout)

[**IaSetTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_settopology)

[**IaSetVertexBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setvertexbuffers)

 

 





