---
title: Automation のテーブルを定義します。
description: Automation のテーブルを定義します。
ms.assetid: 1c0dace6-b618-4705-bf5d-65457d14c072
keywords:
- BDA ミニドライバー WDK AVStream、automation テーブル
- automation の WDK AVStream テーブルにします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9944d2f233d8c8e478a629399ed8d4e2d5cbf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549141"
---
# <a name="defining-automation-tables"></a>Automation のテーブルを定義します。





フィルター、pin、またはノードのオートメーション テーブルは、内容は、フィルター、pin、またはノードでサポートされるメソッドとプロパティについて説明します。 BDA ミニドライバー AVStream によって既に実装されているプロパティまたはメソッドのハンドラーを提供している場合、BDA ミニドライバーの実装には AVStream がより優先されます。

BDA ミニドライバーは、プロパティとメソッドのセットの配列を定義し、配列、ミニドライバーが要求を自動的に処理できるように設定の自動化のテーブルを定義する必要があります。 参照してください、 [BDA デバイス トポロジを決定する](determining-bda-device-topology.md)ミニドライバーもこのセクションを参照に設定されたプロパティを定義する方法の例のセクション。

次のコード スニペットは、プロパティとメソッドのセットの配列とオートメーション テーブルのフィルターの例を示しています。

```cpp
//
//  Filter Level Property Set supported
//
//  This array defines a property set supported by the
//  filter that is exposed by the minidriver.
//
DEFINE_KSPROPERTY_SET_TABLE(FilterPropertySets)
{
    DEFINE_KSPROPERTY_SET
    (
        &KSPROPSETID_BdaTopology,                   // Set
        SIZEOF_ARRAY(FilterTopologyProperties),     // PropertiesCount
        FilterTopologyProperties,                   // PropertyItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Filter Level Method Sets supported
//
//  This array defines method sets supported by the
//  filter that is exposed by the minidriver.
//
DEFINE_KSMETHOD_SET_TABLE(FilterMethodSets)
{
    DEFINE_KSMETHOD_SET
    (
        &KSMETHODSETID_BdaChangeSync,               // Set
        SIZEOF_ARRAY(BdaChangeSyncMethods),         // MethodsCount
        BdaChangeSyncMethods,                       // MethodItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    ),
    DEFINE_KSMETHOD_SET
    (
        &KSMETHODSETID_BdaDeviceConfiguration,      // Set
        SIZEOF_ARRAY(BdaDeviceConfigurationMethods),// MethodsCount
        BdaDeviceConfigurationMethods,              // MethodItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Filter Automation Table
//
//  Lists all arrays of property and method sets for the filter that 
//  is exposed by the minidriver.
//
DEFINE_KSAUTOMATION_TABLE(FilterAutomation) {
    DEFINE_KSAUTOMATION_PROPERTIES(FilterPropertySets),
    DEFINE_KSAUTOMATION_METHODS(FilterMethodSets),
    DEFINE_KSAUTOMATION_EVENTS_NULL
};
```

次のコード スニペットでは、プロパティ セットの配列とノードのオートメーション テーブルの例を示します。

```cpp
//
//  RF tuner node property set supported
//
//  This array defines a property set supported by the
//  RF Tuner Node associated with the antenna input pin.
//
DEFINE_KSPROPERTY_SET_TABLE(RFNodePropertySets)
{
    DEFINE_KSPROPERTY_SET
    (
        &KSPROPSETID_BdaFrequencyFilter,            // Set
        SIZEOF_ARRAY(RFNodeFrequencyProperties),    // PropertiesCount
        RFNodeFrequencyProperties,                  // PropertyItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Radio frequency tuner node automation table
//
//
DEFINE_KSAUTOMATION_TABLE(RFTunerNodeAutomation) {
    DEFINE_KSAUTOMATION_PROPERTIES( RFNodePropertySets),
    DEFINE_KSAUTOMATION_METHODS_NULL,
    DEFINE_KSAUTOMATION_EVENTS_NULL
};
```

 

 




