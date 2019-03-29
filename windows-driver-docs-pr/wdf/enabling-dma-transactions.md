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
ms.openlocfilehash: e75b39f9d1ecb46c5b19bd6f370512ecf0aad033
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570633"
---
# <a name="enabling-dma-transactions"></a>DMA トランザクションの有効化


\[KMDF にのみ適用されます。\]




フレームワークに基づくドライバーでは、DMA デバイスの I/O 操作を処理する場合、ドライバーは、DMA デバイスごとのフレームワークの DMA 機能を有効にする必要があります。 これらを有効にする機能、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)または[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数にする必要があります。

1.  呼び出す[ **WdfDeviceSetAlignmentRequirement** ](https://msdn.microsoft.com/library/windows/hardware/ff546861)バッファーの配置のデバイスの要件を指定します。

2.  呼び出す[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983) DMA 操作 (1 つのパケットまたはスキャッター/ギャザー) と、デバイスをサポートする最大転送サイズの種類を指定します。 フレームワークには、KMDF バージョン 1.11 以降、[システム モードの DMA](supporting-system-mode-dma.md)チップ (SoC) のシステムに – ベースの Windows 8 またはそれ以降のバージョンのオペレーティング システムで実行されているシステム。

3.  呼び出す[ **WdfDmaEnablerSetMaximumScatterGatherElements** ](https://msdn.microsoft.com/library/windows/hardware/ff547014)デバイスは、スキャッター/ギャザーをサポートしている場合は、スキャッター/ギャザーの一覧で、デバイスをサポートできる要素の最大数を指定するには操作です。

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

ドライバーが呼び出された後**WdfDmaEnablerCreate**、呼び出すことができます[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff547020) WDM へのポインターを取得する[ **DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff544062)デバイスの入力と出力方向のフレームワークを作成する構造体。 ただし、ほとんどのフレームワーク ベースのドライバーでは、これらの構造体にアクセスする必要はありません。









