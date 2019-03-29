---
title: KSPROPSETID\_Itd3d
description: KSPROPSETID\_Itd3d
ms.assetid: 87159be4-740e-47c9-b16f-16ca4d01c793
keywords:
- KSPROPSETID_Itd3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3413d7716adb44f851773949acc07be6b6dfa2d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574550"
---
# <a name="kspropsetiditd3d"></a>KSPROPSETID\_Itd3d


## <span id="ddk_kspropsetid_itd3d_ks"></span><span id="DDK_KSPROPSETID_ITD3D_KS"></span>


`KSPROPSETID_Itd3d`プロパティ セットは、3 D のノードで使用される両耳間時間遅延 (ITD) アルゴリズムの構成に使用されます ([**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md))。

リスナーに到達するサウンドの左端し、ソースの位置に応じて異なる量によって、特定のサウンドのソースから右の耳が遅延します。 リスナーは、差分の遅延の長さから音源の方向を推測できます。 ITD アルゴリズムでは、3 D 空間内の特定の場所で音源をシミュレートするために差分の遅延を制御します。

ITD アルゴリズムは、各耳に到達するサウンドのこもった感じされる量を制御することで、追加のサウンド配置キューを提供します。 頻度の高いサウンドは、リスナーの頭の背後にあるサウンドのソースをシミュレートするためにこもった感じことができます。 耳を右側の近くにある音源のなど左耳に到達するサウンドがよりこもった感じより右耳に到達します。 Muffled サウンドは同じ信号の低域フィルター処理されたバージョンといくつかの割合でサウンドのソースから元の信号を組み合わせることによって生成されます。 ソースの移動、シミュレートされたサウンドさらに、リスナーの頭の背後にあるの効果をシミュレートするフィルター選択されたバージョンの低域からの寄与を増やすと、元の信号を減衰させます。

音源の位置が変更されたときに、次のパラメーターを更新する必要があります。

-   各耳に到達するサウンドの遅延の量。

-   各耳に到達するサウンドのこもった感じする量。

これらのパラメーターに瞬間的な変更を加えるには をクリックし、その他の擬似ノイズ可能性があります。 このような音を除外するためにサンプルの数をこれらのパラメーターに ITD アルゴリズムを滑らかに遷移します。

ITD アルゴリズムによって使用されるパラメーターの詳細については、次を参照してください。 [ **KSDS3D\_ITD\_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff537110)します。

このプロパティ セットには、1 つのプロパティのみが含まれています。

[**KSPROPERTY\_ITD3D\_PARAMS**](ksproperty-itd3d-params.md)

 

 





