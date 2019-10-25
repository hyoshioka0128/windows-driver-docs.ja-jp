---
title: ストリーム出力ステージ
description: ストリーム出力ステージ
ms.assetid: e3f4685f-a214-4934-a36f-92591ef99db8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5a38a254ed2cd613a84c62e5be78e80a96e321d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829436"
---
# <a name="stream-output-stage"></a>ストリーム出力ステージ


ストリーム出力 (SO) ステージは、頂点をラスタライザーに到達する直前に、頂点をメモリにストリーミングできます。 ストリーム出力は、パイプラインの tap と同様に動作します。 データがラスタライザーに送られ続ける場合でも、このタップを有効にすることができます。 ストリーム出力を通じて送信されるデータは、バッファーに連結されます。 これらのバッファーは、パイプライン入力として後続のパスで使用できます。

ストリームの出力に関する制約の1つは、それが geometry シェーダーに関連付けられていることです (ただし、これらを一緒に作成する必要がありますが、どちらも "NULL"/"off" にすることができます)。 ただし、にストリーミングされる特定のメモリバッファーは、特定のジオメトリシェーダーとストリーム出力のペアに関連付けられていません。 ストリーム出力にフィードする頂点データの部分の説明だけが、ジオメトリシェーダーに関連付けられています。

ストリーム出力は、再利用される順序付けされたパイプラインデータを保存する場合に便利です。 たとえば、頂点のバッチが "スキン" であるとします。これは、頂点が独立した点であるかのようにパイプラインに渡すことによって、各頂点に "スキニング" 操作を適用し、結果をメモリにストリーミングします。 その後、保存された "スキン" 頂点を入力として使用できるようになります。

ストリーム出力によって書き込まれる出力の量は動的であるため、新しい種類の Draw ( [**Drawauto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)) が必要です。これは、ストリーム出力バッファーを入力アセンブラーで再利用できるようにするためです実際に記述されています。 また、ストリーム出力のオーバーフローを軽減し、ストリーム出力バッファーに書き込まれたデータの量を取得するためにクエリが必要になります (D3D10DDI\_QUERY\_STREAMOVERFLOWPREDICATE and D3D10DDI\_QUERY\_[**D3D10DDI\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)列挙型の STREAMOUTPUTSTATS)。

Direct3D ランタイムは、次のドライバー関数を呼び出して、ストリーム出力を作成および設定します。

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**SoSetTargets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_so_settargets)

 

 





