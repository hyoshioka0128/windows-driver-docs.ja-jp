---
title: DMA トランザクションの有効化
description: DMA トランザクションの有効化
ms.assetid: 87735776-c371-425b-bc53-0c68375c9562
keywords:
- DMA トランザクション WDK KMDF、有効にします。
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 368246e9a5e4dd192bf87bfaad5fc948660711d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368726"
---
# <a name="enabling-dma-transactions"></a>DMA トランザクションの有効化


\[KMDF にのみ適用されます。\]




フレームワークに基づくドライバーでは、DMA デバイスの I/O 操作を処理する場合、ドライバーは、DMA デバイスごとのフレームワークの DMA 機能を有効にする必要があります。 これらを有効にする機能、ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数にする必要があります。

1.  呼び出す[ **WdfDeviceSetAlignmentRequirement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)バッファーの配置のデバイスの要件を指定します。

2.  呼び出す[ **WdfDmaEnablerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) DMA 操作 (1 つのパケットまたはスキャッター/ギャザー) と、デバイスをサポートする最大転送サイズの種類を指定します。 フレームワークには、KMDF バージョン 1.11 以降、[システム モードの DMA](supporting-system-mode-dma.md)チップ (SoC) のシステムに – ベースの Windows 8 またはそれ以降のバージョンのオペレーティング システムで実行されているシステム。

3.  呼び出す[ **WdfDmaEnablerSetMaximumScatterGatherElements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablersetmaximumscattergatherelements)デバイスは、スキャッター/ギャザーをサポートしている場合は、スキャッター/ギャザーの一覧で、デバイスをサポートできる要素の最大数を指定するには操作です。

次のコード例から、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプル フレームワークの DMA の機能を有効にする方法を示しています。 このコードは、 *Init.c ファイル*します。

```cpp
WDF_DMA_ENABLER_CONFIG   dmaConfig;

WdfDeviceSetAlignmentRequirement( DevExt->Device, PCI9656_DTE_ALIGNMENT_16 );
WDF_DMA_ENABLER_CONFIG_INIT( &dmaConfig,
                             WdfDmaProfileScatterGather64Duplex,
                             DevExt->MaximumTransferLength );
status = WdfDmaEnablerCreate( DevExt->Device,
                              &dmaConfig, 
                              WDF_NO_OBJECT_ATTRIBUTES,
                              &DevExt->DmaEnabler );
```

かどうか、ドライバー共通のバッファーが必要、ドライバーの*EvtDriverDeviceAdd*コールバック関数通常それらを設定します。 これらのバッファーの詳細については、次を参照してください。[を使用して一般的なバッファー](using-common-buffers.md)します。

ドライバーが呼び出された後**WdfDmaEnablerCreate**、呼び出すことができます[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter) WDM へのポインターを取得する[ **DMA\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_adapter)デバイスの入力と出力方向のフレームワークを作成する構造体。 ただし、ほとんどのフレームワーク ベースのドライバーでは、これらの構造体にアクセスする必要はありません。









