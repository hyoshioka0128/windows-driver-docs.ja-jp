---
title: HD Audio DDI のルーチン
description: HD Audio DDI のルーチン
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81050764092c336862ab4315a7a1fa88c7b93b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359991"
---
# <a name="hd-audio-ddi-routines"></a>HD Audio DDI のルーチン


説明したよう[の相違点の間、HD オーディオ DDI バージョン](https://docs.microsoft.com/windows-hardware/drivers/audio/differences-between-the-hd-audio-ddi-versions)、HD オーディオ DDI の 3 つのバージョンが存在します。 これら 3 つの DDI バージョンがによって定義されている、 [ **HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [ **HDAUDIO\_BUS\_インターフェイス\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)、および[ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体。

DDI の 3 つのバージョンでは、カーネル モードでのみアクセスできます。

各 DDI バージョンでは、HD オーディオ バス コント ローラーを管理するハードウェア リソースへのアクセスを提供します。 これらのリソースには、コーデックには、DMA エンジンには、リンクの帯域幅には、リンク位置レジスタ、ウォール クロックの登録が含まれます。 HD オーディオ バス ドライバーでは、DDI を実装し、その子に DDI を公開します。 子は、DDI を使用して、HD オーディオ コント ローラーに接続されているハードウェアのコーデックを管理するカーネル モード機能のドライバーのインスタンスです。

DDI バージョンへのアクセスを取得するには、関数のドライバーが DDI コンテキスト オブジェクトの HD オーディオ バス ドライバーのクエリを実行する必要があります。 詳細については、次を参照してください[取得、HDAUDIO\_バス\_インターフェイス DDI オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-ddi-object)、 [、HDAUDIO を取得する\_バス\_インターフェイス\_V2 DDI オブジェクト。](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-v2-ddi-object)、および[、HDAUDIO を取得する\_BUS\_インターフェイス\_BDL DDI オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-bdl-ddi-object)します。

コンテキスト オブジェクトへのポインターは、3 つの DDI バージョンの各ルーチンは、その最初の呼び出しのパラメーターとして受け取ります。

HDAUDIO\_BUS\_インターフェイス構造体は、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

HDAUDIO\_BUS\_インターフェイス\_V2 構造体には、Windows Vista および以降のバージョンの Windows、および、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer_with_notification)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer_with_notification)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**RegisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_notification_event)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

[**UnregisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_notification_event)

HDAUDIO\_BUS\_HD オーディオ DDI のインターフェイスのバージョンが Windows Vista および Windows の以降のバージョンでサポートされています。 さらに、この DDI をサポートしている HD オーディオ バス ドライバーのバージョンは、Windows 2000、Windows XP、および Windows Server 2003 にインストールできます。

HDAUDIO\_BUS\_インターフェイス\_BDL 構造は、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

HDAUDIO をサポートしている HD オーディオ バス ドライバーのバージョン\_BUS\_インターフェイス\_HD オーディオ DDI の BDL バージョンは、Windows 2000、Windows XP、および Windows Server 2003 にインストールできます。 ただし、Windows Vista にはこの DDI バージョンのサポートはありません。

2 つの Ddi のルーチンのほとんどは、名前と操作の両方で同じです。 ただし、HDAUDIO の一部である次の 2 つルーチン\_BUS\_DDI のバージョンのインターフェイスを HDAUDIO に含まれない\_BUS\_インターフェイス\_BDL バージョン。

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

次に示す 3 つルーチン、HDAUDIO で同様に、\_BUS\_インターフェイス\_DDI の BDL バージョンは、HDAUDIO の一部ではない\_BUS\_インターフェイスのバージョン。

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

このセクションでは、次の DDI ルーチンについて説明します。

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)効果的な[ **PHDAUDIO\_BDL\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-phdaudio_bdl_isr)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

上記の一覧には、DDI のいずれかまたは両方のバージョンで表示されるすべてのルーチンが含まれています。

 

 





