---
title: BDA デバイス トポロジの決定
description: BDA デバイス トポロジの決定
ms.assetid: fdac317e-d4fc-47c9-87d3-bec597f758f5
keywords:
- メソッドは、WDK BDA、BDA デバイス トポロジを設定します。
- プロパティは、WDK BDA、BDA デバイス トポロジを設定します。
- KSPROPERTY_BDA_NODE_TYPES
- KSPROPERTY_BDA_PIN_TYPES
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS
- テンプレート フィルター トポロジ WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e9fd63ba928358c3ae5395f3a3544c04c29ae1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374068"
---
# <a name="determining-bda-device-topology"></a>BDA デバイス トポロジの決定





BDA デバイスのトポロジは、シグナルへの変換を表す各ノードの接続されたネットワークで構成されます。 ノードは、さまざまなフィルター間で任意にグループ化できます。 この任意のグループ化には、実装方法、ハードウェアとドライバーをサポートするネットワークのさまざまな種類のネットワーク プロバイダーを使用した一般的な方法でこのようなハードウェアとドライバーが処理できるように特定の自由でハードウェア ベンダーが提供します。

この任意のグループ化アーキテクチャが機能するには、ネットワーク プロバイダーは変換の種類 (つまり、どのような種類のノードのネットワーク フィルター サポートできる) シグナルへのこれらのフィルターを実行するためのクエリ フィルターすることにあります。 フィルターの基になるリング 0 ミニドライバーを使用して、ネットワーク プロバイダーに、サポートされているノードのネットワークの図の伝達、 [KSPROPSETID\_BdaTopology](https://msdn.microsoft.com/library/windows/hardware/ff566561)プロパティ セット。

ネットワーク プロバイダーがノードの種類のリストを反復処理のフィルターのテンプレートのトポロジを決定するときに、暗証番号 (pin) の型し各ノードとその機能の暗証番号 (pin) クエリを実行します。 ネットワーク プロバイダー KSPROPSETID の次のプロパティを使用して\_BdaTopology フィルターのテンプレートのトポロジを決定します。

-   KSPROPERTY\_BDA\_ノード\_型

    ノードの種類は、フィルター内で実行可能な機能のノードを表します。 KSPROPERTY\_BDA\_ノード\_型のプロパティが BDA ミニドライバーのフィルターのインスタンスによって提供されるすべてのノード型の一覧を返します。 ミニドライバーは、ノードの種類を識別するために任意の値を割り当てます。 通常、ミニドライバーの各要素のインデックス ミニドライバーのノードの種類の一覧で値として使用、それぞれのノード型。 BDA ミニドライバーでは、ノードの種類ごとに、ノードの記述を GUID が割り当てられます。 ネットワーク プロバイダーは現在サポートされている型が定義されているノードの説明 Guid *bdamedia.h*します。 このノードの説明は、ネットワーク プロバイダーにノードにはどのようなことを示します。 テンプレートのトポロジでは、ノード タイプは 1 回だけ発生します。 ただし、特定の種類の 1 つ以上のノードには、同じノードの説明の GUID があります。 これにより、一方で、1 つのトポロジ ノードを明確に識別するために、ネットワーク プロバイダー、フィルターのトポロジでは、複数の場所に存在する特定の信号変換できます。

-   KSPROPERTY\_BDA\_PIN\_型

    暗証番号 (pin) の型は、グラフ内の他のフィルターに使用可能な接続を表します。 KSPROPERTY\_BDA\_PIN\_型のプロパティは、フィルターを作成できるすべてのピンの種類の一覧を返します。 テンプレートのトポロジでは、暗証番号 (pin) の型は 1 回だけ発生します。

-   KSPROPERTY\_BDA\_テンプレート\_接続

    KSPROPERTY\_BDA\_テンプレート\_接続プロパティのノード型と、フィルターを構成できる暗証番号 (pin) 型の使用可能なすべての接続を表す配列を返します。 参照してください[接続トポロジのマッピング](mapping-connection-topology.md)詳細についてはします。

フィルター インスタンスは最初に作成され、グラフに追加、ときに、通常に、入力ピン、出力ピンはないです。 出力ピンを作成するには、ネットワーク プロバイダー最初に使用して、KSPROPSETID\_BdaTopology プロパティをフィルターが実行できる操作を確認します。 これらのプロパティからは、ネットワーク プロバイダーは、グラフでは特定のフィルターを実行するフィルターが必要ですがどのような操作を決定します。 ネットワーク プロバイダーを使用し、 [KSMETHODSETID\_BdaDeviceConfiguration](https://msdn.microsoft.com/library/windows/hardware/ff563404)ピン留めする特定の種類に対応する出力ピンを作成し、実際のハードウェアのパスの間は、内部のトポロジを作成する方法の設定これらのピンと pin を入力します。 参照してください[BDA フィルターを構成する](configuring-a-bda-filter.md)詳細についてはします。

次のコード スニペットは、KSPROPSETID のディスパッチ ルーチンとして BDA サポート ライブラリによってエクスポートされる関数を定義する方法を示します\_BdaTopology プロパティ セット。

```cpp
//
//  KSPROPSETID_BdaTopology property set
//
//  Defines the dispatch routines for the filter level
//  topology properties
//
DEFINE_KSPROPERTY_TABLE(FilterTopologyProperties)
{
    DEFINE_KSPROPERTY_ITEM_BDA_NODE_TYPES(
        BdaPropertyNodeTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_PIN_TYPES(
        BdaPropertyPinTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_TEMPLATE_CONNECTIONS(
        BdaPropertyTemplateConnections,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_CONTROLLING_PIN_ID(
        BdaPropertyGetControllingPinId,
        NULL
        )
};
```

 

 




