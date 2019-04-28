---
title: KSPROPSETID\_BdaTopology
description: KSPROPSETID\_BdaTopology
ms.assetid: 26d67e68-56a9-4d36-9e33-6fb4486d7cd9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d240bf2601d66448b2d6b66017fd313f7f509b9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382508"
---
# <a name="kspropsetidbdatopology"></a>KSPROPSETID\_BdaTopology


## <span id="ddk_kspropsetid_bdatopology_ks"></span><span id="DDK_KSPROPSETID_BDATOPOLOGY_KS"></span>


KSPROPSETID\_BdaTopology は BDA トポロジのプロパティ セット。 機能の詳細についてフィルターを照会するために使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_NODE_TYPES"></span><span id="ksproperty_bda_node_types"></span>[**KSPROPERTY\_BDA\_ノード\_型**](ksproperty-bda-node-types.md)  
ノードの種類の一覧を返します。

<span id="KSPROPERTY_BDA_PIN_TYPES"></span><span id="ksproperty_bda_pin_types"></span>[**KSPROPERTY\_BDA\_PIN\_型**](ksproperty-bda-pin-types.md)  
暗証番号 (pin) の種類の一覧を返します。

<span id="KSPROPERTY_BDA_TEMPLATE_CONNECTIONS"></span><span id="ksproperty_bda_template_connections"></span>[**KSPROPERTY\_BDA\_テンプレート\_接続**](ksproperty-bda-template-connections.md)  
Pin とテンプレートのトポロジのノード間の接続の一覧を返します。

<span id="KSPROPERTY_BDA_NODE_METHODS"></span><span id="ksproperty_bda_node_methods"></span>[**KSPROPERTY\_BDA\_ノード\_メソッド**](ksproperty-bda-node-methods.md)  
ノードでサポートされるメソッドの一覧を返します。

<span id="KSPROPERTY_BDA_NODE_PROPERTIES"></span><span id="ksproperty_bda_node_properties"></span>[**KSPROPERTY\_BDA\_ノード\_プロパティ**](ksproperty-bda-node-properties.md)  
ノードでサポートされるプロパティの一覧を返します。

<span id="KSPROPERTY_BDA_NODE_EVENTS"></span><span id="ksproperty_bda_node_events"></span>[**KSPROPERTY\_BDA\_ノード\_イベント**](ksproperty-bda-node-events.md)  
ノードでサポートされているイベントの一覧を返します。

<span id="KSPROPERTY_BDA_CONTROLLING_PIN_ID"></span><span id="ksproperty_bda_controlling_pin_id"></span>[**KSPROPERTY\_BDA\_制御\_PIN\_ID**](ksproperty-bda-controlling-pin-id.md)  
BDA テンプレートの接続の一覧で、ノードの制御の暗証番号 (pin) を返します。

<span id="KSPROPERTY_BDA_NODE_DESCRIPTORS"></span><span id="ksproperty_bda_node_descriptors"></span>[**KSPROPERTY\_BDA\_ノード\_記述子**](ksproperty-bda-node-descriptors.md)  
ノードの一覧を返します。

### <a name="comments"></a>コメント

BDA サポート ライブラリは、このプロパティのセットを処理するために既定のメソッドを提供します。 ネットワーク プロバイダーのフィルターは、このプロパティが、フィルター、メソッド、プロパティおよび pin ノードごとにサポートされているイベントのテンプレートのトポロジを決定する設定を使用します。 ネットワーク プロバイダーのフィルターでは、このノードと暗証番号 (pin) 情報を使用して、操作の種類フィルターは信号に対して実行できると、グラフにフィルターを追加するかどうかを調べます。 フィルターの実際のトポロジは、ネットワーク プロバイダーがフィルターで実際に行われた、暗証番号 (pin) とノードの接続を指します。

このプロパティ セット内のプロパティは、フィルターが実行できる内容を定義します。 通常、フィルターでは、これらのプロパティのいずれか傍受する必要はありません。 詳細については、次を参照してください。[ドライバー アーキテクチャ ミニドライバーのブロードキャスト](https://msdn.microsoft.com/library/windows/hardware/ff556588)フィルター BDA ミニドライバーが関数の BDA サポート ライブラリを使用して、これらのプロパティの既定の処理を提供する方法にします。 ドライバー ライターでは、このプロパティ セットの処理を有効にする静的構造を作成する必要があります。 これらの構造が作成され、BDA サポート ライブラリに登録されている、ドライバーの作成者がこのプロパティのセットをサポートするには、さらに何もする必要はありません。

 

 





