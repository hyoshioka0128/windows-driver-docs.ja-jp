---
title: KSPROPSETID\_BdaNullTransform
description: KSPROPSETID\_BdaNullTransform
ms.assetid: 08277c76-4fa5-46d0-8c86-4bc0e060fa9c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8514f5555bfa1d5a013b360a5cd8bf5c65dd43d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574331"
---
# <a name="kspropsetidbdanulltransform"></a>KSPROPSETID\_BdaNullTransform


## <span id="ddk_kspropsetid_bdanulltransform_ks"></span><span id="DDK_KSPROPSETID_BDANULLTRANSFORM_KS"></span>


KSPROPSETID\_BdaNullTransform は、BDA **null**プロパティ セットを変換します。 ノードが、変更なしの信号を渡すよう指示するために使用されます。 以降、 **NULL**ノードでの変換がないその他の関数では、その出力を入力からの直接接続に効果的にノードを変更します。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_START"></span><span id="ksproperty_bda_null_transform_start"></span>[**KSPROPERTY\_BDA\_NULL\_変換\_開始**](ksproperty-bda-null-transform-start.md)  
ノードが以前、信号に適用し、ノードを通過する信号をできることをいずれかの変換を無効に変更されていません。

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_STOP"></span><span id="ksproperty_bda_null_transform_stop"></span>[**KSPROPERTY\_BDA\_NULL\_変換\_停止**](ksproperty-bda-null-transform-stop.md)  
再起動、KSPROPERTY で変換が無効にする前に、シグナルへのノードが実行される変換\_BDA\_NULL\_変換\_START プロパティ。

### <a name="comments"></a>コメント

ネットワーク プロバイダーのフィルターには、このプロパティのノードが対応しているネットワーク プロバイダーは、変更せずその特定のノードを通過する信号を必要がある場合は、設定を使用できます。

 

 





