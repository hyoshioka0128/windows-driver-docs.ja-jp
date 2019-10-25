---
title: KSPROPSETID\_Itd3d
description: KSPROPSETID\_Itd3d
ms.assetid: 87159be4-740e-47c9-b16f-16ca4d01c793
keywords:
- KSPROPSETID_Itd3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2cb80d8c307059f79d463c1611bf2691ebbf6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830469"
---
# <a name="kspropsetid_itd3d"></a>KSPROPSETID\_Itd3d


## <span id="ddk_kspropsetid_itd3d_ks"></span><span id="DDK_KSPROPSETID_ITD3D_KS"></span>


`KSPROPSETID_Itd3d` プロパティセットは、3D ノード ([**KSNODETYPE\_3d\_効果**](ksnodetype-3d-effects.md)) で使用される耳より time DELAY (ITD) アルゴリズムを構成するために使用されます。

リスナーの左側と右の耳に到達する音は、ソースの位置によって異なります。 リスナーは、サウンドソースの方向を、差分遅延の量から推測できます。 ITD アルゴリズムは、3D 空間内の特定の位置にあるサウンドソースをシミュレートするための差分を制御します。

ITD アルゴリズムでは、各 ear に到達する音が muffled になる量を制御することで、追加のサウンド配置キューを提供します。 高頻度のサウンドは、リスナーの頭の背後にあるサウンドソースをシミュレートするために muffled することができます。 たとえば、右耳の近くにあるサウンドソースの場合、左耳に達したサウンドは、右耳に到達するよりも muffled が高くなります。 Muffled サウンドは、サウンドソースからの元の信号を、同じシグナルの低パスのフィルター選択されたバージョンと組み合わせることによって生成されます。 低パスのフィルター選択されたバージョンからの貢献度を上げるときに元のシグナルを Attenuating すると、シミュレートされたサウンドソースをリスナーの先頭の背後に移動した場合の効果がシミュレートされます。

サウンドソースの位置が変更された場合は、次のパラメーターを更新する必要があります。

-   サウンドが各 ear に到達するまでの遅延時間。

-   各イヤーに到達する音の量は muffled です。

これらのパラメーターを瞬時に変更すると、クリックやその他の疑似音が発生する可能性があります。 ITD アルゴリズムは、このようなノイズをフィルターで除外するために、これらのパラメーターを多数のサンプルにわたって滑らかに切り替えます。

ITD アルゴリズムによって使用されるパラメーターの詳細については、「 [**KSDS3D\_ITD\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params)」を参照してください。

このプロパティセットには、1つのプロパティのみが含まれます。

[**KSK プロパティ\_ITD3D\_PARAMS**](ksproperty-itd3d-params.md)

 

 





