---
title: KSPROPSETID\_BdaAutodemodulate
description: KSPROPSETID\_BdaAutodemodulate
ms.assetid: b7c3c934-5b31-48da-9fb0-98007267711b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6ed1fe40e0511e1fcde416be0907067678eef15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548958"
---
# <a name="kspropsetidbdaautodemodulate"></a>KSPROPSETID\_BdaAutodemodulate


## <span id="ddk_kspropsetid_bdaautodemodulate_ks"></span><span id="DDK_KSPROPSETID_BDAAUTODEMODULATE_KS"></span>


KSPROPSETID\_BdaAutodemodulate は BDA autodemodulate プロパティのセット。 変調された信号の特性を確認および復調が行われずできる自動的にシグナル復調器ノードの制御に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_AUTODEMODULATE_START"></span><span id="ksproperty_bda_autodemodulate_start"></span>[**KSPROPERTY\_BDA\_AUTODEMODULATE\_開始**](ksproperty-bda-autodemodulate-start.md)  
を一時停止または実行の状態のときは、する必要がありますを試みることに自動的に変調パラメーターの確認および復調信号が行われず、復調器ノードに通知します。

<span id="KSPROPERTY_BDA_AUTODEMODULATE_STOP"></span><span id="ksproperty_bda_autodemodulate_stop"></span>[**KSPROPERTY\_BDA\_AUTODEMODULATE\_停止**](ksproperty-bda-autodemodulate-stop.md)  
自動的に復調信号が行われずにしようとして停止する必要があります復調器ノードに通知します。

### <a name="comments"></a>コメント

KSPROPSETID\_BdaAutodemodulate は復調器ノードの場合のみ変調パラメーターの 1 つの構成をサポートする 8VSB 復調器ノードなども使用されます。 これらのノードの種類に対して、復調器は Inner および Outer の転送エラー訂正 (FEC) メソッドなどの特定の値を設定するのには通知されません。

 

 





