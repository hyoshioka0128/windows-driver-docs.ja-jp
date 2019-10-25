---
title: DMA トランザクションの有効化
description: DMA トランザクションの有効化
ms.assetid: 87735776-c371-425b-bc53-0c68375c9562
keywords:
- DMA トランザクション WDK KMDF、有効化
- DMA 操作 WDK KMDF、トランザクション
- バスマスタ DMA WDK KMDF、トランザクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e507648cd48cddbdfc8dfcded0e9bad9b10eca1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842857"
---
# <a name="enabling-dma-transactions"></a>DMA トランザクションの有効化


\[は KMDF にのみ適用され\]




フレームワークベースのドライバーが DMA デバイスの i/o 操作を処理する場合、ドライバーは各 DMA デバイスに対してフレームワークの DMA 機能を有効にする必要があります。 これらの機能を有効にするには、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で次のことを行う必要があります。

1.  [**Wdfdevicesetalignment 要件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)を呼び出して、バッファーの配置に関するデバイスの要件を指定します。

2.  [**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出して、DMA 操作の種類 (単一パケットまたはスキャッター/ギャザー) と、デバイスがサポートする最大転送サイズを指定します。 KMDF バージョン1.11 以降では、フレームワークは、Windows 8 以降のバージョンのオペレーティングシステムで実行されているチップ (SoC) ベースのシステム上の[システムモードの DMA](supporting-system-mode-dma.md)をサポートしています。

3.  デバイスでスキャッター/ギャザー操作がサポートされている場合は、 [**WdfDmaEnablerSetMaximumScatterGatherElements**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablersetmaximumscattergatherelements)を呼び出して、スキャッター/gather リストでデバイスがサポートできる要素の最大数を指定します。

[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの次のコード例は、フレームワークの DMA 機能を有効にする方法を示しています。 このコードは、*初期 .c ファイル*に記述されています。

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

ドライバーに共通のバッファーが必要な場合は、通常、ドライバーの*Evtdriverdeviceadd*コールバック関数によって設定されます。 これらのバッファーの詳細については、「[共通バッファーの使用](using-common-buffers.md)」を参照してください。

ドライバーが**WdfDmaEnablerCreate**を呼び出した後、 [**WdfDmaEnablerWdmGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)を呼び出して、デバイスの入出力方向用にフレームワークによって作成された WDM [**DMA\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)構造へのポインターを取得できます。 ただし、ほとんどのフレームワークベースのドライバーは、これらの構造体にアクセスする必要がありません。









