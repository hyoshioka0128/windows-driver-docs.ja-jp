---
title: GPU エンジンの機能の列挙
description: Windows 8.1 以降、ディスプレイのミニポート ドライバーは GPU のノードのエンジンの機能のクエリを実行するために使用 DxgkDdiGetNodeMetadata 関数に実装する必要があります。
ms.assetid: 822FEB3E-A39D-4B33-BD9D-F3166EF99AF8
keywords:
- GPU ノード、WDK のディスプレイ ドライバーを列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 448e1d347a6252e1197e4304eb6afebafadd22b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353906"
---
# <a name="enumerating-gpu-engine-capabilities"></a>GPU エンジンの機能の列挙


Windows 8.1 以降、ディスプレイのミニポート ドライバーを実装する必要があります、 [ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)関数で、GPU のノードのエンジンの機能のクエリを実行するために使用します。

この情報は、ワークロードがスケジュールされ、ノード間で分散する方法の評価に役立ち、アプリケーションをデバッグする機能を改善します。

## <a name="span-idenginecapabilitiesdevicedriverinterfaceddispanspan-idenginecapabilitiesdevicedriverinterfaceddispanspan-idenginecapabilitiesdevicedriverinterfaceddispanengine-capabilities-device-driver-interface-ddi"></a><span id="Engine_capabilities_device_driver_interface__DDI_"></span><span id="engine_capabilities_device_driver_interface__ddi_"></span><span id="ENGINE_CAPABILITIES_DEVICE_DRIVER_INTERFACE__DDI_"></span>エンジンの機能のデバイス ドライバー インターフェイス (DDI)


このインターフェイスは、GPU の指定されたノードのエンジンの機能を提供します。

-   [*DxgkDdiGetNodeMetadata*](https://msdn.microsoft.com/library/windows/hardware/dn265415)
-   [**DXGKARG\_GETNODEMETADATA**](https://msdn.microsoft.com/library/windows/hardware/dn265405)
-   [**DXGK\_エンジン\_型**](https://msdn.microsoft.com/library/windows/hardware/dn265417)

ポインター、 [ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)によって関数が提供される、 **DxgkDdiGetNodeMetadata**のメンバー、 [**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)構造体。

## <a name="span-idgpunodearchitecturespanspan-idgpunodearchitecturespanspan-idgpunodearchitecturespangpu-node-architecture"></a><span id="GPU_node_architecture"></span><span id="gpu_node_architecture"></span><span id="GPU_NODE_ARCHITECTURE"></span>GPU ノードのアーキテクチャ


システムでは、各ディスプレイ アダプターが、さまざまな異なるエンジンでタスクをスケジュールできます。 各エンジンは、1 つのノードに割り当てられているが、各ノードはそのノードに複数のアダプターに関連付けられている場合は、複数のエンジンを含めることができます: リンクの表示 (LDA) アダプターの構成、複数の物理 Gpu が 1 つの高速化、仮想のフォームにリンクされてなどGPU します。

![gpu エンジンとノードのアーキテクチャ](images/gpu-engine-node-architecture.png)

別のノードは、GPU の非対称の処理のコアを表し、各ノード内のエンジンがアダプター間で対称的な処理のコアを表します。 つまり、3-D のノードには、複数のアダプターとしない別のエンジンの種類上の同一 3-D エンジンのみが含まれます。

エンジンは常にグループ化ノードのエンジンの種類によって、ため、指定したノードに基づく、エンジンの種類の情報を照会できます。 ディスプレイのミニポート ドライバーを指定できますエンジンの種類が記載されて、 [ **DXGK\_エンジン\_型**](https://msdn.microsoft.com/library/windows/hardware/dn265417)列挙体。

## <a name="span-idexampleimplementationofnodemetadatafunctionspanspan-idexampleimplementationofnodemetadatafunctionspanspan-idexampleimplementationofnodemetadatafunctionspanexample-implementation-of-node-metadata-function"></a><span id="Example_implementation_of_node_metadata_function"></span><span id="example_implementation_of_node_metadata_function"></span><span id="EXAMPLE_IMPLEMENTATION_OF_NODE_METADATA_FUNCTION"></span>ノードのメタデータ関数の実装例


このコードは、ディスプレイのミニポート ドライバーを実装によって返されることがあるエンジンの種類のいくつかの方法を示しています、 [ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)関数。

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

 

 





