---
title: DMA デバイスの電源管理のサポート
description: DMA デバイスの電源管理のサポート
ms.assetid: abbb8f60-560f-41c9-85c5-1ec82078b99e
keywords:
- DMA 操作 WDK KMDF、電源管理
- バスマスタ DMA WDK KMDF、電源管理
- 電源管理 WDK KMDF、DMA デバイス
- DMA イネーブラーオブジェクト WDK KMDF
- enabler オブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c4175035dcf51c015f0c88f50a467f2144ed8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831697"
---
# <a name="supporting-power-management-for-dma-devices"></a>DMA デバイスの電源管理のサポート


\[は KMDF にのみ適用され\]

DMA イネーブラーオブジェクトは、オプションのイベントコールバック関数のセットを定義します。この関数は、DMA デバイス用のドライバーが、デバイスの動作 (D0) 状態との間の遷移を管理するために使用できます。

DMA デバイスが動作状態になるたびに、フレームワークがドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) callback 関数を呼び出した後、次の DMA コールバック関数が一覧表示された順序で呼び出されます。

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)  
デバイスの DMA バッファーを割り当てます。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)  
デバイスが動作中 (D0) 状態になった後に、デバイスの DMA 機能を有効にします。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)  
DMA デバイスの自己管理型 i/o 操作を開始します。

DMA デバイスが動作状態を抜けるたびに、フレームワークがドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数を呼び出した前に、次の dma コールバック関数が一覧表示された順序で呼び出されます。

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)  
DMA デバイスの自己管理型 i/o 操作を停止します。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)  
デバイスの動作 (D0) 状態が出る前に、デバイスの DMA 機能を無効にします。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)  
デバイスの DMA バッファーの割り当てを解除します。

フレームワークがドライバーのイベントコールバック関数を呼び出す順序の詳細については、「 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)」を参照してください。

 

 





