---
title: アダプター オブジェクトの概要
description: アダプター オブジェクトの概要
ms.assetid: a1a0d516-dee0-484a-b971-c7a595fef155
keywords:
- AdapterControl ルーチン、AdapterControl ルーチンについて
- DMA 転送 WDK カーネル、アダプターオブジェクト
- アダプタオブジェクト WDK カーネル、アダプタオブジェクトについて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dd589a676a4d1e2b0785d5b52a4426ed86ca863
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838635"
---
# <a name="introduction-to-adapter-objects"></a>アダプター オブジェクトの概要





ダイレクト i/o と DMA を使用するドライバーでは、アダプターオブジェクトを作成する必要があります。 アダプターオブジェクトは、DMA コントローラーチャネルまたはポート、またはバスマスタデバイスを表します。

2種類の下位レベルのドライバーでは、アダプターオブジェクトを使用する必要があります。

-   システム DMA コントローラーを使用するデバイスのドライバー。 このようなデバイスは "*下位デバイス*" と呼ばれ、"システム (または*下位*) DMA を使用" と呼ばれます。

-   バスマスターアダプターであるデバイスのドライバー。 このようなデバイスは、i/o バスを使用するためにシステムを調停するため、バスマスタ DMA を使用します。

ドライバーは、アダプターオブジェクトへのポインターのストレージ (通常はデバイス拡張機能) を提供します。

DMA 転送を実行するために、これらの DMA メソッドのいずれかを使用するデバイスのドライバーは、通常、 [*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンを持ち、アダプターオブジェクトを操作するシステム提供のサポートルーチンを呼び出します。 ( *Adaptercontrol*ルーチンを必要としないドライバーには、[スキャッター/ギャザー dma を使用](using-scatter-gather-dma.md)するドライバーと[、一般的なバッファー、バスマスタ dma を使用](using-common-buffer-bus-master-dma.md)するドライバーが含まれます)。

デバイスのスタートアップ操作の一部として、DMA 操作を処理するドライバーは、i/o マネージャーを呼び出し、その後、プラットフォーム固有の HAL を呼び出して一連のアダプターオブジェクトを作成します。 すべての Windows プラットフォームで、アダプターオブジェクトのセットには、通常、次のためのアダプターオブジェクトが含まれています。

-   下位デバイスが接続されている各システム DMA コントローラーチャネルまたはポート。

-   コンピューターの各バスマスタ DMA デバイス。

(バスマスタ DMA 対応の SCSI デバイスの場合、SCSI ポートドライバーは、HBA 固有の SCSI ミニポートドライバー用のアダプターオブジェクトを設定します。 ミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンは、ポートドライバーにアダプター固有のデータを提供します)。

ドライバーがアダプタオブジェクトと*Adaptercontrol*ルーチンを使用するタイミングと方法の詳細については、「[システム Dma](using-system-dma.md)と[バスマスタ DMA](using-bus-master-dma.md)の使用」を参照してください。

 

 




