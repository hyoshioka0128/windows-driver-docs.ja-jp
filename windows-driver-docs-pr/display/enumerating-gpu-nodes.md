---
title: GPU エンジンの機能の列挙
description: Windows 8.1 以降では、ディスプレイミニポートドライバーは、GPU ノードのエンジン機能に対してクエリを実行するために使用される DxgkDdiGetNodeMetadata 関数を実装する必要があります。
ms.assetid: 822FEB3E-A39D-4B33-BD9D-F3166EF99AF8
keywords:
- GPU ノード、WDK ディスプレイドライバーの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be67ffb243bd76975a46c88405f02028afc6adcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838955"
---
# <a name="enumerating-gpu-engine-capabilities"></a>GPU エンジンの機能の列挙


Windows 8.1 以降では、ディスプレイミニポートドライバーは、GPU ノードのエンジン機能に対してクエリを実行するために使用される[*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)関数を実装する必要があります。

この情報は、ワークロードがノード間でスケジュールおよび配布される方法を評価し、アプリケーションのデバッグ機能を向上させるのに役立ちます。

## <a name="span-idengine_capabilities_device_driver_interface__ddi_spanspan-idengine_capabilities_device_driver_interface__ddi_spanspan-idengine_capabilities_device_driver_interface__ddi_spanengine-capabilities-device-driver-interface-ddi"></a><span id="Engine_capabilities_device_driver_interface__DDI_"></span><span id="engine_capabilities_device_driver_interface__ddi_"></span><span id="ENGINE_CAPABILITIES_DEVICE_DRIVER_INTERFACE__DDI_"></span>エンジン機能デバイスドライバーインターフェイス (DDI)


このインターフェイスは、指定された GPU ノードのエンジン機能を提供します。

-   [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)
-   [**DXGKARG\_GETNODEMETADATA**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGK\_ENGINE\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-dxgk_engine_type)

[*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)関数へのポインターは、[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造体の**DxgkDdiGetNodeMetadata**メンバーによって提供されます。

## <a name="span-idgpu_node_architecturespanspan-idgpu_node_architecturespanspan-idgpu_node_architecturespangpu-node-architecture"></a><span id="GPU_node_architecture"></span><span id="gpu_node_architecture"></span><span id="GPU_NODE_ARCHITECTURE"></span>GPU ノードのアーキテクチャ


システム上の各ディスプレイアダプターには、のタスクをスケジュールするために使用できるさまざまなエンジンが用意されています。 各エンジンは1つのノードにのみ割り当てられますが、1つのノードに複数のアダプター (リンクされたディスプレイアダプター (LDA) 構成など) が関連付けられている場合は、複数の物理 Gpu がリンクされていて、1つの高速、仮想を形成します。GPU.

![gpu エンジンとノードのアーキテクチャ](images/gpu-engine-node-architecture.png)

ノードごとに、GPU の非対称処理コアを表します。各ノード内のエンジンは、アダプター間の対称処理コアを表します。 つまり、3d ノードには、複数のアダプターに同一の3-d エンジンのみが含まれ、エンジンの種類は異なります。

エンジンは常にエンジンの種類によってノードにグループ化されるため、エンジンの種類の情報は、指定されたノードに基づいてクエリを実行できます。 ディスプレイミニポートドライバーが指定できるエンジンの種類は、 [**DXGK\_engine\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-dxgk_engine_type)列挙に一覧表示されます。

## <a name="span-idexample_implementation_of_node_metadata_functionspanspan-idexample_implementation_of_node_metadata_functionspanspan-idexample_implementation_of_node_metadata_functionspanexample-implementation-of-node-metadata-function"></a><span id="Example_implementation_of_node_metadata_function"></span><span id="example_implementation_of_node_metadata_function"></span><span id="EXAMPLE_IMPLEMENTATION_OF_NODE_METADATA_FUNCTION"></span>ノードメタデータ関数の実装例


このコードは、 [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)関数によって返される可能性のあるエンジンの種類の一部を、表示ミニポートドライバーで実装する方法を示しています。

```ManagedCPlusPlus
NTSTATUS
IHVGetNodeDescription(
        IN_CONST_HANDLE                     hAdapter,
        UINT                                NodeOrdinal,
        OUT_PDXGKARG_GETNODEMETADATA        pGetNodeMetadata
        )
{
    DDI_FUNCTION();
    PAGED_CODE();

    if(NULL == pGetNodeMetadata)
    {
        return STATUS_INVALID_PARAMETER;
    }

    CAdapter *pAdapter = GetAdapterFromHandle(hAdapter);

    //Invalid handle
    if(NULL == pAdapter)
    {
        return STATUS_INVALID_PARAMETER;
    }

    //Node ordinal is out of bounds. Required to return
    //STATUS_INVALID_PARAMETER
    if(NodeOrdinal >= pAdapter->GetNumNodes())
    {
        return STATUS_INVALID_PARAMETER;
    }

    switch(pAdapter->GetEngineType(NodeOrdinal))
    {
        //This is the adapter's 3-D engine. This engine handles a large number
        //of different workloads, but it also handles the adapter's 3-D 
        //workloads. Therefore the 3-D capability is what must be exposed.
        case GPU_ENGINE_3D:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_3D;
            break;
        }

        //This is the adapter's video decoding engine
        case GPU_ENGINE_VIDEO_DECODE:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_VIDEO_DECODE;
            break;
        }

        //This engine is proprietary and contains no functionality that
        //fits the DXGK_ENGINE_TYPE enumeration
        case GPU_ENGINE_PROPRIETARY_ENGINE_1:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_OTHER;

            //Copy over friendly name associated with this engine
            SetFriendlyNameForEngine(pGetNodeMetadata->FriendlyName,
                                     DXGK_MAX_METADATA_NAME_LENGTH,
                                     PROPRIETARY_ENGINE_1_NAME);
            break;
        }
    }

    return STATUS_SUCCESS;
}
```

 

 





