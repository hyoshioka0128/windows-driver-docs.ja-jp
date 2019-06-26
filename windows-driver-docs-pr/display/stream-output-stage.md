---
title: ストリーム出力ステージ
description: ストリーム出力ステージ
ms.assetid: e3f4685f-a214-4934-a36f-92591ef99db8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68d6c9d68887d412a6c068c1471acaa84cf3648d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364362"
---
# <a name="stream-output-stage"></a>ストリーム出力ステージ


ストリーム出力 (、) ラスタライザーにこれらの頂点が到着する前に、ステージがメモリに頂点をストリーミングできます。 ストリーム出力は、パイプラインでのタップのように動作します。 ラスタライザーまでフローにデータが継続しても、このタップをオンにすることができます。 ストリーム出力を介して送信されるデータは、バッファーに連結されます。 これらのバッファーは、パイプラインの入力として後続のパスで再利用できます。

ストリームに関する制約は 1 つの出力をまとめて作成する必要があります、ジオメトリ シェーダーに関連付けられていることが (ただし、NULL 値が""「オフ」/)。 ストリーム出力する特定のメモリ バッファーではありませんが、特定のジオメトリ シェーダーとストリーム出力のペアに関連付けられています。 のみ、ジオメトリ シェーダーに関連付けられている出力ストリームにフィードする頂点データのどの部分の説明です。

ストリーム出力が再利用される順序付けされたパイプラインのデータを保存するために便利ですがあります。 たとえば、頂点のバッチ可能性があります「スキンにする」をパイプラインに頂点を渡すように独立したポイント (それらのすべてを 1 回アクセス) には、各頂点で「スキニング」操作の適用、メモリに結果をストリーミングしています。 「スキン」を保存した頂点は入力として使用するため、その後に使用できます。

ストリーム出力の最後まで書き込まれた出力の量が動的であるため、新しい種類の描画、 [ **DrawAuto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)、せず、入力のアセンブラーで再利用をストリーム出力バッファーを許可する必要がありますデータの量が実際に書き込まれたかを決定する CPU 関与します。 さらに、クエリは、ストリーム出力のオーバーフローの軽減し、データの量は、ストリーム出力バッファーに書き込まれたかを取得するために必要な (D3D10DDI\_クエリ\_STREAMOVERFLOWPREDICATE と D3D10DDI\_クエリ\_STREAMOUTPUTSTATS、 [ **D3D10DDI\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)列挙型)。

Direct3D ランタイムでは、ストリーム出力を作成および設定には、次のドライバー関数を呼び出します。

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**SoSetTargets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_so_settargets)

 

 





