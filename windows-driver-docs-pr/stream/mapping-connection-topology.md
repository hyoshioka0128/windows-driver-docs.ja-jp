---
title: 接続トポロジのマッピング
description: 接続トポロジのマッピング
ms.assetid: f11ffc48-a117-4b75-bc19-7a3762e6ba19
keywords:
- メソッドは、WDK BDA、接続トポロジのマッピングを設定します。
- プロパティは、WDK BDA、接続トポロジのマッピングを設定します。
- WDK BDA トポロジ
- 接続トポロジのマッピング
- 接続トポロジの WDK BDA のマッピング
- BDA_TEMPLATE_CONNECTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a929406b41c719dbf76f5b617f0906d39361691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386639"
---
# <a name="mapping-connection-topology"></a>接続トポロジのマッピング





BDA サポート ライブラリ プロパティとメソッドに代わって BDA ミニドライバー リング 3 でのアプリケーションを提供するためには、BDA ミニドライバーは BDA サポート ライブラリへの接続トポロジのマッピングを指定する必要があります。 BDA ミニドライバーの配列では、このマッピングを提供する[ **BDA\_テンプレート\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_template_connection)構造体。 BDA ミニドライバー渡しますこの BDA\_テンプレート\_接続配列の配列の[ **KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection) を呼び出すときに構造体[ **BdaCreateFilterFactory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdacreatefilterfactory)関数をサポートします。 参照してください[開始 BDA ミニドライバー](starting-a-bda-minidriver.md)詳細についてはします。 この配列は、フィルターまたはフィルターおよび隣接するフィルターの間に作成できるノードと暗証番号 (pin) の型の間のすべての使用可能な接続の表現を提供します。

ネットワーク プロバイダーのフィルターは、KSPROPERTY こと、その後\_BDA\_テンプレート\_の接続プロパティの要求、 [KSPROPSETID\_BdaTopology](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-bdatopology)プロパティ フィルターの設定ミニドライバーの接続トポロジを取得する BDA ミニドライバーのインスタンス。 さらに BDA ミニドライバー、 [ **BdaPropertyTemplateConnections** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertytemplateconnections)フィルターのテンプレートの接続の一覧を返す関数をサポート (BDA\_テンプレート\_接続の構造) KSTOPOLOGY の配列で\_接続構造体。 Bda メンバー\_テンプレート\_接続構造が次の接続の種類をノードと pin のペアを識別します。

-   接続の開始位置、ノードと暗証番号 (pin) の種類

-   接続の終了位置となるノードと暗証番号 (pin) の種類

− 1 の値に、ノードの種類を設定するには、接続を開始またはそれぞれ上流または下流のいずれかのフィルターの暗証番号 (pin) で終了することを示します。 それ以外の場合、ノード型の値は、内部ノード型の 0 から始まる配列内の要素のインデックスに対応します。 この配列の配列は、 [ **KSNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)構造体。 暗証番号 (pin) 型の値は、テンプレートのフィルター記述子 BDA ミニドライバーをで使用可能な暗証番号 (pin) 型の 0 から始まる配列内の要素のインデックスに対応します。 この配列の配列は、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。

次のコード スニペットは、ノードの種類と BDA ミニドライバーのフィルター記述子をテンプレートで使用可能な暗証番号 (pin) 型の配列などを示しています。

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

次のコード スニペットでは、配列のテンプレートの接続および結合の例を示します。

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

 

 




