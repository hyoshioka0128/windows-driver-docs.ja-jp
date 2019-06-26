---
title: DMA デバイスの電源管理のサポート
description: DMA デバイスの電源管理のサポート
ms.assetid: abbb8f60-560f-41c9-85c5-1ec82078b99e
keywords:
- DMA 操作 WDK KMDF、電源管理
- バス マスター DMA WDK KMDF、電源管理
- 電源管理 WDK KMDF、DMA デバイス
- DMA イネーブラー オブジェクト WDK KMDF
- WDK KMDF のオブジェクトの有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3800f26cbbe5626bfd6bda2925ff40708fdccc20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368049"
---
# <a name="supporting-power-management-for-dma-devices"></a>DMA デバイスの電源管理のサポート


\[KMDF にのみ適用されます。\]

DMA イネーブラー オブジェクトでは、DMA デバイス用のドライバーに、およびデバイスの操作 (D0) 状態からの移行を管理に使用できる省略可能なイベントのコールバック関数のセットを定義します。

DMA デバイスは、州、およびフレームワークの後にその作業を入力するたびに、ドライバーが呼び出されて[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数では、フレームワークが呼び出す DMA コールバック関数を次に、一覧の順序:

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)  
デバイスの DMA バッファーを割り当てます。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)  
デバイスの作業 (D0) 状態に入った後は、デバイスの DMA の機能を有効にします。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)  
DMA デバイスの自己管理型の I/O 操作を開始します。

州、およびフレームワークの前に、DMA デバイスがその作業を離れるたびに、ドライバーが呼び出されて[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数では、フレームワークが呼び出す DMA コールバック関数を次に、一覧の順序:

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)  
DMA デバイスの自己管理型の I/O 操作を停止します。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)  
デバイスがその作業 (D0) 状態を抜ける前に、デバイスの DMA の機能を無効にします。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)  
デバイスの DMA バッファーの割り当てを解除します。

これで、フレームワーク ドライバーのイベントのコールバック関数、順序の詳細については、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

 

 





