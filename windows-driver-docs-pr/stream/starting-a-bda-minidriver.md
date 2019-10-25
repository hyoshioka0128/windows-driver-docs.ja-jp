---
title: BDA ミニドライバーの起動
description: BDA ミニドライバーの起動
ms.assetid: c71e1483-756c-4e98-a413-64ff02ee4a9b
keywords:
- BDA ミニドライバー WDK AVStream、開始
- BDA ミニドライバー WDK AVStream を開始しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb26d511dd464ceb3213af7d50252872355c6104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837699"
---
# <a name="starting-a-bda-minidriver"></a>BDA ミニドライバーの起動





BDA デバイスが動作を開始すると、プラグアンドプレイ (PnP) マネージャーは、 [ **\_デバイスの開始\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)をディスパッチします。 AVStream クラスは、BDA デバイスに関連付けられている BDA ミニドライバーの開始ルーチンを呼び出します。 この開始ルーチンは、レジストリからデバイスに関する情報を取得し、デバイスに関する情報を設定した後、 [**Bdacreatefilterfactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory)サポート関数を呼び出して次のことを行います。

-   デバイスの初期フィルター記述子 ([**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)) からデバイスのフィルターファクトリを作成します。 初期フィルター記述子は、フィルターおよび入力ピンのディスパッチテーブルとオートメーションテーブルを参照します。 詳細については、「[ディスパッチテーブルを作成する](creating-dispatch-tables.md)」および「[オートメーションテーブルを定義](defining-automation-tables.md)する」を参照してください。

-   フィルターファクトリを[**BDA\_フィルター\_テンプレート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)構造に関連付けます。 この構造体は、デバイスのテンプレートフィルター記述子と、使用可能な入力ピンと出力ピンのペアの一覧を参照します。 次に、この記述子とリストのリファレンスを示します。
    -   ネットワークプロバイダーが BDA フィルターのトポロジを決定するために使用できる静的テンプレート構造。
    -   ノードとは、フィルターを接続するために使用できる方法と共に、BDA フィルターをピン留めします。
    -   フィルターインスタンスを作成して閉じるためにネットワークプロバイダーが使用できるルーチン。
    -   ネットワークプロバイダーが BDA フィルターを操作するために使用できる静的テンプレート構造。
-   Bda\_FILTER\_テンプレートによって指定された静的なテンプレート構造を BDA サポートライブラリと共に登録して、ライブラリが BDA ミニドライバーのプロパティとメソッドの既定の処理を提供できるようにします。

次のコードスニペットは、フィルターファクトリとして**Bdacreatefilterfactory**セットを設定するデバイスの初期フィルター記述子の例を示しています。

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

次のコードスニペットは、初期化されたフィルターによって公開される初期 pin 記述子の配列の例を示しています。 ネットワークプロバイダーは、このような配列を使用してフィルターを初期化してから、ネットワークプロバイダーがそのフィルターを構成します。 ただし、初期化されたフィルターを構成する場合、ネットワークプロバイダーは、BDA\_フィルター\_テンプレート構造のフィルター記述子メンバーへのポインターで参照されているピンを選択します。 詳細について[は、「BDA フィルターの構成](configuring-a-bda-filter.md)」を参照してください。

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

初期化されたフィルターには1つ以上の入力ピンが公開されていなければならないことに注意してください。これにより、Microsoft DirectShow **IFilterMapper2**または**ifiltermapper**インターフェイスでそのフィルターを見つけることができます これらの DirectShow インターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

次のコードスニペットは、BDA\_フィルター\_テンプレート構造と関連する構造体および配列の例を示しています。

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

 

 




