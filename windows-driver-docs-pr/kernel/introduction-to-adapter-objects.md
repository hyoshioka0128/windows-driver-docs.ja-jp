---
title: アダプター オブジェクトの概要
description: アダプター オブジェクトの概要
ms.assetid: a1a0d516-dee0-484a-b971-c7a595fef155
keywords:
- AdapterControl ルーチンについての AdapterControl ルーチン
- DMA は、WDK カーネルでは、アダプタ オブジェクトを転送します。
- アダプター オブジェクトについて、アダプター オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31ac4e12cb2be8461be0d06dd61d653f83737664
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341068"
---
# <a name="introduction-to-adapter-objects"></a>アダプター オブジェクトの概要





ダイレクト I/O および DMA を使用する任意のドライバーでは、アダプター オブジェクトを作成する必要があります。 アダプター オブジェクトでは、dma コント ローラーまたはポート、またはバス マスター デバイスのいずれかを表します。

最下位レベルのドライバーの 2 つの種類には、アダプター オブジェクトを使用する必要があります。

-   システムの DMA コント ローラーを使用するデバイス ドライバーです。 このようなデバイスと呼びます*デバイスを下位*呼ば"システムを使用して (または*下位*) DMA"。

-   バス マスター アダプターをデバイスのドライバーです。 このようなデバイスでは、システム I/O バスの使用を調停および、したがってバス マスター DMA を使用します。

ドライバーは、アダプター オブジェクトへのポインターのデバイスの拡張機能では、通常のストレージを提供します。

通常、これらの DMA メソッドのいずれかを使用するデバイスのドライバーがある DMA の転送を実行する、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチンとアダプター オブジェクトを操作するシステム提供のサポート ルーチンを呼び出し。 (ドライバーを必要としない*AdapterControl*ルーチンを[使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)とそれらを[共通バッファー、バス マスター DMA を使用して、](using-common-buffer-bus-master-dma.md))。

デバイスの起動操作、ハンドルの DMA 操作を呼び出す必要が I/O マネージャー、ドライバーの一部としては、アダプター オブジェクトのセットを作成するプラットフォームに固有の HAL の呼び出しで有効にします。 任意の Windows プラットフォームでアダプター オブジェクトのセットには、アダプター オブジェクトには通常が含まれます。

-   各システム DMA コント ローラーのチャネルまたは下位のデバイスが接続されているポート。

-   コンピューター内の各のバス マスター DMA デバイス

(バス マスター DMA の対応の SCSI デバイスの SCSI ポート ドライバーを設定、ミニポート ドライバーの HBA に固有の SCSI アダプター オブジェクト。 ミニポート ドライバーの[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチンは、ポート使用してドライバーをアダプターに固有のデータを提供します)。

参照してください[システム DMA を使用して](using-system-dma.md)と[バス マスター DMA を使用して](using-bus-master-dma.md)ドライバーがアダプター オブジェクトを使用するタイミングと方法の詳細については、 *AdapterControl*ルーチン。

 

 




