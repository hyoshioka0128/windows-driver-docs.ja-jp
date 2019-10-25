---
title: KSPROPSETID\_Hrtf3d
description: KSPROPSETID\_Hrtf3d
ms.assetid: 8045991b-0409-445a-bd35-d9b8644f770e
keywords:
- KSPROPSETID_Hrtf3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 210a1002b65c040c4fd4c53f04454867b6383acd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830474"
---
# <a name="kspropsetid_hrtf3d"></a>KSPROPSETID\_Hrtf3d


## <span id="ddk_kspropsetid_hrtf3d_ks"></span><span id="DDK_KSPROPSETID_HRTF3D_KS"></span>


`KSPROPSETID_Hrtf3d` プロパティセットは、DirectSound バッファーの3D ヘッド相対転送関数 (HRTF) を構成するために使用されます。 このセットには、DirectSound pin インスタンス上の3D ノード ([**KSNODETYPE\_3d\_効果**](ksnodetype-3d-effects.md)) のオプションのプロパティが含まれています。

すべての3D ノードで HRTF 処理がサポートされるわけではありません。 クライアントは、HRTF プロパティの基本的なサポートクエリを3D ノードに送信して、そのノードが HRTF 処理を実行できるかどうかを判断できます。 `KSPROPSETID_Hrtf3d` プロパティセットをサポートする3D ノードでは、セット内の3つのプロパティすべてがサポートされている必要があります。

このプロパティセットの定義では、1つの位置でのオーディオソースの効果を表す無限インパルス応答 (IIR) フィルターを使用して、HRTF アルゴリズムが実装されていることを前提としています。

デジタルフィルターには、通常、最初の一時的な応答があります。 ある位置から次の位置にソースを移動すると、フィルター係数が変化し、HRTF アルゴリズムによって、古い位置にあるフィルターから新しい位置のフィルターに出力がクロスフェードされます。 [**KSDS3D\_HRTF\_INIT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)構造体**のメンバーは、新しい**フィルターの初期の一時が表示されないように、クロスフェードを遅延するサンプルの数を指定します。 この期間中、出力は古いフィルターのみに由来します。 **FilterOverlapBufferLength**メンバー (同じ構造体) は、フィルター出力をミュートおよびクロスフェードするサンプルの合計数を指定します。

ソースが右半分から左へ移動すると、フィルターが切り替わります。 このスイッチにより、可聴 pop が発生する可能性があります。 [**KSDS3D\_HRTF\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)構造体の**swapchannels**メンバーは、出力をスワップして、ソースの場所を他の半平面に戻すように HRTF アルゴリズムに指示します。 **クロス Fadeoutput**メンバー (同じ構造体) は、azimuth アングルゼロ間の遷移後に出力チャネルをクロスフェードするようにアルゴリズムに指示します。 KSDS3D\_HRTF\_INIT\_MSG の**OutputOverlapBufferLength**メンバーは、この遷移が発生したときにクロスフェードするサンプルの数を指定します。

対称であるため、azimuth angle がゼロの場合は、フィルター係数の半分だけを HRTF アルゴリズムにダウンロードする必要があります。 KSDS3D\_HRTF\_PARAMS\_MSG の**ZeroAzimuth**メンバーは、この状態が発生したことを示します。

DirectSound API を使用した HTRF 処理の構成の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

`KSPROPSETID_Hrtf3d` プロパティセットには、次の3つのメンバーが含まれています。

[**KSK プロパティ\_HRTF3D\_フィルター\_形式**](ksproperty-hrtf3d-filter-format.md)

[**KSK プロパティ\_HRTF3D\_INITIALIZE**](ksproperty-hrtf3d-initialize.md)

[**KSK プロパティ\_HRTF3D\_PARAMS**](ksproperty-hrtf3d-params.md)

 

 





