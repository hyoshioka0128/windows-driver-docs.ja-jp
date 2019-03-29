---
title: BDA ミニドライバーの起動
description: BDA ミニドライバーの起動
ms.assetid: c71e1483-756c-4e98-a413-64ff02ee4a9b
keywords:
- BDA ミニドライバー WDK AVStream、開始
- BDA ミニドライバー WDK AVStream の開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a63e9266792f5248da35d7009b0f9970a8fd56e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582235"
---
# <a name="starting-a-bda-minidriver"></a>BDA ミニドライバーの起動





BDA デバイスの運用開始時に、プラグ アンド プレイ (PnP) マネージャーのディスパッチ[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)します。 AVStream クラスは、BDA デバイスに関連付けられた BDA ミニドライバーの開始ルーチンを呼び出します。 この開始ルーチン レジストリからデバイスに関する情報を取得、デバイスに関する情報を設定およびを呼び出して、 [ **BdaCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff556438)に関数をサポートします。

-   最初のフィルター記述子からデバイスのフィルター ファクトリの作成 ([**KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)) デバイス。 最初のフィルター記述子は、フィルターおよび入力ピンのディスパッチと自動化のテーブルを参照します。 参照してください[ディスパッチ テーブルを作成](creating-dispatch-tables.md)と[Automation テーブルを定義する](defining-automation-tables.md)詳細についてはします。

-   フィルター ファクトリに関連付ける、 [ **BDA\_フィルター\_テンプレート**](https://msdn.microsoft.com/library/windows/hardware/ff556523)構造体。 この構造体は、デバイスと、入力と出力ピンの考えられるペアの一覧のテンプレートのフィルター記述子を参照します。 この記述子と一覧がさらに参照します。
    -   ネットワーク プロバイダーが BDA フィルターのトポロジの決定に使用できる静的テンプレート構造体。
    -   ノードと、フィルターを接続する方法と共に BDA フィルターの pin。
    -   ネットワーク プロバイダーが作成し、フィルターのインスタンスを閉じるに使用できるルーチン。
    -   ネットワーク プロバイダーは、BDA フィルターの操作に使用できる静的テンプレート構造体。
-   BDA で指定されている静的テンプレート構造体を登録\_フィルター\_ライブラリは、既定の BDA ミニドライバーのプロパティとメソッドの処理を提供できるように、BDA でテンプレートがライブラリをサポートします。

次のコード スニペットの例を示します、デバイスの最初のフィルター記述子を**BdaCreateFilterFactory**フィルター ファクトリとして設定します。

```cpp
const KSFILTER_DESCRIPTOR    InitialTunerFilterDescriptor;
//
//  Filter Factory Descriptor for the tuner filter
//
//  This structure brings together all of the structures that define
//  the tuner filter instance as it appears when it is first created.
//  Note that not all template pin and node types are exposed as
//  pin and node factories when the filter instance is created.
//
DEFINE_KSFILTER_DESCRIPTOR(InitialTunerFilterDescriptor)
{
    &FilterDispatch,             // Table of dispatch routines
    &FilterAutomation,           // Table of properties and methods
    KSFILTER_DESCRIPTOR_VERSION, // Version
    0,                           // Flags
    &KSNAME_Filter,              // Reference Guid
    DEFINE_KSFILTER_PIN_DESCRIPTORS(InitialPinDescriptors),
                                   // PinDescriptorsCount
                                   // PinDescriptorSize
                                   // PinDescriptors
    DEFINE_KSFILTER_CATEGORY(KSCATEGORY_BDA_RECEIVER_COMPONENT),
                            // CategoriesCount
                            // Categories
    DEFINE_KSFILTER_NODE_DESCRIPTORS_NULL(NodeDescriptors),
                                    // NodeDescriptorsCount
                                    // NodeDescriptorSize
                                    // NodeDescriptors
    DEFINE_KSFILTER_DEFAULT_CONNECTIONS, // ConnectionsCount
                                         // Connections
    NULL                // ComponentId
};
```

次のコード スニペットでは、初期化済みのフィルターによって公開されている最初の pin 記述子の配列の例を示します。 ネットワーク プロバイダーには、ネットワーク プロバイダーは、そのフィルターを構成する前に、このような配列を使用してフィルターを初期化します。 ただし、初期化済みのフィルターを構成するときに、ネットワーク プロバイダーを選択しますピンが参照されている、BDA のフィルター記述子のメンバーへのポインターで\_フィルター\_テンプレート構造体。 参照してください[BDA フィルターを構成する](configuring-a-bda-filter.md)詳細についてはします。

```cpp
//
//  Initial Pin Descriptors
//
//  This data structure defines the pins that will appear on the 
//  filter when it is first created.
//
const
KSPIN_DESCRIPTOR_EX
InitialPinDescriptors[] =
{
    //  Antenna Pin
    //
    {
        &AntennaPinDispatch,
        &AntennaAutomation,   // AntennaPinAutomation
        {
            0,  // Interfaces
            NULL,
            0,  // Mediums
            NULL,
            SIZEOF_ARRAY(AntennaPinRanges),
            AntennaPinRanges,
            KSPIN_DATAFLOW_IN,
            KSPIN_COMMUNICATION_BOTH,
            NULL,   // Name
            NULL,   // Category
            0
        },
        KSPIN_FLAG_DO_NOT_USE_STANDARD_TRANSPORT | 
        KSPIN_FLAG_FRAMES_NOT_REQUIRED_FOR_PROCESSING | 
        KSPIN_FLAG_FIXED_FORMAT,
        1,      // InstancesPossible
        0,      // InstancesNecessary
        NULL,   // Allocator Framing
        NULL    // PinIntersectHandler
    }
};
```

初期化済みのフィルターが 1 つのまたは複数の入力ピンが公開されていることに注意してくださいように Microsoft DirectShow **IFilterMapper2**または**IFilterMapper**インターフェイスは、そのフィルターを見つけることができます。 これらの DirectShow インターフェイスについては、Microsoft Windows SDK ドキュメントを参照してください。

次のコード スニペットは、BDA の例を示します\_フィルター\_テンプレートの構造と関連構造と配列。

```cpp
const KSFILTER_DESCRIPTOR  TemplateTunerFilterDescriptor;
const BDA_PIN_PAIRING  *TemplateTunerPinPairings;
//
//  BDA Template Topology Descriptor for the filter factory.
//
//  This structure defines the pin and node types that the network 
//  provider can create on the filter and how they are arranged. 
//
const
BDA_FILTER_TEMPLATE
TunerBdaFilterTemplate =
{
    &TemplateTunerFilterDescriptor,
    SIZEOF_ARRAY(TemplateTunerPinPairings),
    TemplateTunerPinPairings
};
//
//  Filter Factory Descriptor for the tuner filter template topology
//
//  This structure brings together all of the structures that define
//  the topologies that the tuner filter can assume as a result of
//  pin factory and topology creation methods.
//
DEFINE_KSFILTER_DESCRIPTOR(TemplateTunerFilterDescriptor)
{
    &FilterDispatch,             // Table of dispatch routines
    &FilterAutomation,           // Table of properties and methods
    KSFILTER_DESCRIPTOR_VERSION, // Version
    0,                           // Flags
    &KSNAME_Filter,              // Reference Guid
    DEFINE_KSFILTER_PIN_DESCRIPTORS(TemplatePinDescriptors),
                                   // PinDescriptorsCount
                                   // PinDescriptorSize
                                   // PinDescriptors
    DEFINE_KSFILTER_CATEGORY(KSCATEGORY_BDA_RECEIVER_COMPONENT),
                            // CategoriesCount
                            // Categories
    DEFINE_KSFILTER_NODE_DESCRIPTORS(NodeDescriptors),  
                                    // NodeDescriptorsCount
                                    // NodeDescriptorSize
                                    // NodeDescriptors
    DEFINE_KSFILTER_CONNECTIONS(TemplateTunerConnections),
                               // ConnectionsCount
                               // Connections
    NULL                // ComponentId
};
//
//  Lists how pairs of input and output pins are configured. 
//
//  Values given to the BDA_PIN_PAIRING structures in the list inform 
//  the network provider which nodes get duplicated when more than one 
//  output pin type is connected to a single input pin type or when
//  more that one input pin type is connected to a single output pin 
//  type. Also, informs of the joints array.
//
const
BDA_PIN_PAIRING TemplateTunerPinPairings[] =
{
    //  Antenna to Transport Topology Joints
    //
    {
        0,  // ulInputPin
        1,  // ulOutputPin
        1,  // ulcMaxInputsPerOutput
        1,  // ulcMinInputsPerOutput
        1,  // ulcMaxOutputsPerInput
        1,  // ulcMinOutputsPerInput
        SIZEOF_ARRAY(AntennaTransportJoints),   // ulcTopologyJoints
        AntennaTransportJoints                  // pTopologyJoints
    }
};
```

 

 




