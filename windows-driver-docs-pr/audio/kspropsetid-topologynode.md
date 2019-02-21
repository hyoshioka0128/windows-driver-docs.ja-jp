---
title: KSPROPSETID\_TopologyNode
description: KSPROPSETID\_TopologyNode
ms.assetid: 0b6696aa-e80d-4806-9fbb-7de701164877
keywords:
- KSPROPSETID_TopologyNode
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cec754c4ba7567e511d5692c4324dc65d3daeec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535920"
---
# <a name="kspropsetidtopologynode"></a>KSPROPSETID\_TopologyNode


## <span id="ddk_kspropsetid_topologynode_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGYNODE_KS"></span>


`KSPROPSETID_TopologyNode`プロパティ セットは、さまざまなトポロジのノードに汎用的な制御を提供します。 トポロジ ノードの種類の一覧は、次を参照してください。[オーディオ トポロジ ノード](audio-topology-nodes.md)します。 このセット内のプロパティは、有効化、無効にするには、トポロジのノードをリセットするために使用します。

システムに、AEC (アコースティック エコー キャンセル) ハードウェア アクセラレータを公開する、オーディオ ドライバーが AEC とノイズ抑制ノードを実装する必要があります ([**KSNODETYPE\_音響\_エコー\_キャンセル** ](ksnodetype-acoustic-echo-cancel.md)と[ **KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)) を有効にして、を通じてこれらのノードの無効化をサポートする必要があります`KSPROPSETID_TopologyNode`プロパティ。 詳細については、次を参照してください。 [Exposing Hardware-Accelerated キャプチャ効果](https://msdn.microsoft.com/library/windows/hardware/ff536379)します。

A [ **KSNODETYPE\_PROLOGIC\_エンコーダー** ](ksnodetype-prologic-encoder.md)ノードをサポートする必要がありますも、`KSPROPSETID_TopologyNode`プロパティ。

`KSPROPSETID_TopologyNode`プロパティ セットには、次のプロパティが含まれています。

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

 

 





