---
title: AVStream でのミューテックスの処理
description: AVStream でのミューテックスの処理
ms.assetid: dd84fe3f-352e-4641-99d7-792ccecb0b40
keywords:
- AVStream ミューテックス WDK
- mutex WDK AVStream
- mutex の処理の WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a430808e2602c2978caf33d3e892413d8a2fd7cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823752"
---
# <a name="processing-mutex-in-avstream"></a>AVStream でのミューテックスの処理





3番目のミューテックスは処理ミューテックスです。 個々のフィルターとピンには、独自の処理ミューテックスがあります。 AVStream は、処理に関連する構造へのアクセスを同期するために、フィルターおよび pin レベルで処理される前に処理ミューテックスを個別に取得します。 AVStream は、パイプセクションへのピンのバインド、スリープまたはスリープ解除の電源操作、記述子の変更など、他の操作中にも処理ミューテックスを取得します。 ミニドライバーは、手動でミューテックスを取得して、処理や記述子の変更などの同期操作を実行できます。 ミニドライバーは、処理と同時に発生しない変更を行う前に、処理ミューテックスを取得する必要があります。

他の2種類のミューテックスと同様に、ミューテックスの処理は再帰的には取得されません。 つまり、ミニドライバーが処理中に処理ミューテックスを取得しようとすると、デッドロックが発生します。

長時間にわたって処理を中断するために処理ミューテックスを使用しないでください。 代わりに、 **Ksgate * Xxx*** 関数を使用して、処理制御ゲートを直接操作します。

処理ミューテックスを取得したスレッドは、その後フィルターコントロールのミューテックスを取得しようとすることはできません。

処理ミューテックスを操作するには、次の関数を使用します。

[**KsFilterAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilteracquireprocessingmutex)、 [**KsPinAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquireprocessingmutex)、 [**ksfilterreleaseprocessingmutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterreleaseprocessingmutex)、 [**KsPinReleaseProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinreleaseprocessingmutex)

 

 




