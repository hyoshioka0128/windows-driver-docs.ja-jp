---
title: 接続トポロジのマッピング
description: 接続トポロジのマッピング
ms.assetid: f11ffc48-a117-4b75-bc19-7a3762e6ba19
keywords:
- メソッドは WDK BDA を設定し、接続トポロジをマッピングします。
- プロパティ設定 WDK BDA, 接続トポロジのマッピング
- トポロジ WDK BDA
- 接続トポロジのマッピング
- 接続トポロジのマッピング WDK BDA
- BDA_TEMPLATE_CONNECTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b332abd5689cbc915a632ffd7de3be0cd277841
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838043"
---
# <a name="mapping-connection-topology"></a>接続トポロジのマッピング





Bda サポートライブラリで、BDA ミニドライバーの代わりに、リング3のアプリケーションにプロパティとメソッドを提供するには、bda ミニドライバーがその接続トポロジと BDA サポートライブラリとのマッピングを提供する必要があります。 BDA ミニドライバーは、このマッピングを、 [**bda\_テンプレート\_の接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)構造体の配列に提供します。 BDA ミニドライバーは、この BDA\_テンプレート\_接続の配列に渡します。この配列は、 [**Bdacreatefilterfactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory)サポート関数を呼び出すときに、 [**kstopology\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)構造体の配列に渡します。 詳細について[は、「BDA ミニドライバーの開始](starting-a-bda-minidriver.md)」を参照してください。 この配列は、フィルター内、またはフィルターと隣接するフィルターの間で可能な、ノードとピンの種類の間で可能なすべての接続の表現を提供します。

その後、ネットワークプロバイダーフィルターは、ミニドライバーを取得するために、BDA プロパティ\_を bda\_テンプレート\_[\_](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-bdatopology) CONNECTIONS プロパティに設定して、bda のフィルターインスタンスに設定する必要があります。ミニドライバーの接続トポロジ。 さらに、BDA ミニドライバーは[**BdaPropertyTemplateConnections**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertytemplateconnections) support 関数を呼び出します。この関数は、KSTOPOLOGY 配列にあるフィルターのテンプレート接続 (BDA\_テンプレート\_接続構造) の一覧を返し\_接続構造体。 BDA\_テンプレート\_の接続構造のメンバーは、接続のノードと pin の種類の次のペアを識別します。

-   接続を開始するノードとピンの種類

-   接続が終了するノードとピンの種類

ノードの種類を−1に設定すると、接続が開始または終了するのは、上流または下流のフィルターのいずれかのピンであることを示します。 それ以外の場合、ノード型の値は、内部ノード型の0から始まる配列内の要素のインデックスに対応します。 この配列は、 [**Ksk ノード\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)の構造体の配列です。 ピンの種類の値は、BDA ミニドライバーのテンプレートフィルター記述子で使用できるピンの種類の0から始まる配列内の要素のインデックスに対応します。 この配列は、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の配列です。

次のコードスニペットは、BDA ミニドライバーのテンプレートフィルター記述子で使用できるノード型とピンの種類の配列の例を示しています。

```cpp
//
//  Template Node Descriptors
//
//  This array describes all Node Types available in the template
//  topology of the filter.
//
const
KSNODE_DESCRIPTOR
NodeDescriptors[] =
{
    {   // 0 node type
        &RFTunerNodeAutomation,// PKSAUTOMATION_TABLE AutomationTable;
        &KSNODE_BDA_RF_TUNER,  // Type
        NULL                   // Name
    },
    {   // 1 node type
        &VSB8DemodulatorNodeAutomation, // PKSAUTOMATION_TABLE 
                                        // AutomationTable;
        &KSNODE_BDA_8VSB_DEMODULATOR,   // Type
        NULL                            // Name
    }
};
//
//  Template Pin Descriptors
//
//  This data structure defines the pin types available in the filters
//  template topology. These structures will be used to create a
//  pin factory ID for a pin type when BdaMethodCreatePin is called.
//
const
KSPIN_DESCRIPTOR_EX
TemplatePinDescriptors[] =
{
    //  Antenna Pin
    //  0 pin type
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
    },

    //  Transport Pin
    //  1 pin type
    {
        &TransportPinDispatch,
        &TransportAutomation,   // TransportPinAutomation
        {
            0,  // Interfaces
            NULL,
            1,  // Mediums
            &TransportPinMedium,
            SIZEOF_ARRAY(TransportPinRanges),
            TransportPinRanges,
            KSPIN_DATAFLOW_OUT,
            KSPIN_COMMUNICATION_BOTH,
            (GUID *) &PINNAME_BDA_TRANSPORT,   // Name
            (GUID *) &PINNAME_BDA_TRANSPORT,   // Category
            0
        },
        KSPIN_FLAG_DO_NOT_USE_STANDARD_TRANSPORT | 
        KSPIN_FLAG_FRAMES_NOT_REQUIRED_FOR_PROCESSING | 
        KSPIN_FLAG_FIXED_FORMAT,
        1,
        1,      // InstancesNecessary
        NULL,   // Allocator Framing
        NULL    // PinIntersectHandler
    }
};
```

次のコードスニペットは、テンプレート接続と結合の配列の例を示しています。

```cpp
//
//  BDA Template Topology Connections
//
//  Lists the possible connections between pin types and
//  node types. This structure along with the BDA_FILTER_TEMPLATE, 
//  KSFILTER_DESCRIPTOR, and BDA_PIN_PAIRING structures 
//  describe how topologies are created in the filter.
//
const
KSTOPOLOGY_CONNECTION TemplateTunerConnections[] =
{
    { -1,  0,  0,  0}, // from upstream filter to 0 pin of 0 node 
    {  0,  1,  1,  0}, // from 1 pin of 0 node to 0 pin of 1 node 
    {  1,  1,  -1, 1}, // from 1 pin of 1 node to downstream filter 
};
//
//  Lists the template joints between antenna (input) and transport 
//  (output) pin types. Values given to joints correspond to indexes 
//  of elements in the preceding KSTOPOLOGY_CONNECTION array.
// 
//  For this template topology, the RF node (0) belongs to the antenna 
//  pin and the 8VSB demodulator node (1) belongs to the transport pin
//
const
ULONG   AntennaTransportJoints[] =
{
    1  // Second element in the preceding KSTOPOLOGY_CONNECTION array.
};
```

 

 




