---
title: AVStream でのミューテックスの処理
description: AVStream でのミューテックスの処理
ms.assetid: dd84fe3f-352e-4641-99d7-792ccecb0b40
keywords:
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- ミュー テックス WDK AVStream の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1222e8ba8f8b43a139213f0aeb7acffcfdd810c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379062"
---
# <a name="processing-mutex-in-avstream"></a>AVStream でのミューテックスの処理





3 番目のミュー テックスは、処理のミュー テックスです。 個別のフィルターと pin が独自の処理のミュー テックスがあります。 AVStream 独立していない処理ミュー テックスを獲得、フィルターと pin のレベルで処理する前に処理に関連する構造体へのアクセスを同期するためにします。 AVStream も処理ミュー テックスを獲得パイプ セクションへのピンのバインドを含むその他の操作中に、スリープ状態または電源の操作をスリープ解除し、記述子を変更します。 ミニドライバーは、処理操作または記述子の変更など、同期操作を実行するミュー テックスを取得手動でことができます。 変更の処理と同時に発生することはできませんが、前に、ミニドライバーは処理ミュー テックスを取得する必要があります。

など、他の 2 種類のミュー テックス、ミュー テックスの処理を再帰的には取得できません。 これは、ミニドライバーは、処理中に処理するミュー テックスを取得しようとする場合、デッドロックが発生したことを意味します。

長期間の処理を中断する処理のミュー テックスを使わないでください。 使用して直接処理制御ゲートを代わりに、操作、 **KSGATE * Xxx*** 関数。

スレッド処理のミュー テックスで取得した後でしようとしないでくださいフィルター コントロール ミュー テックスを取得します。

処理のミュー テックスを操作するには、次の関数を使用します。

[**KsFilterAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilteracquireprocessingmutex)、 [ **KsPinAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinacquireprocessingmutex)、 [ **KsFilterReleaseProcessingMutex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterreleaseprocessingmutex)、 [ **KsPinReleaseProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinreleaseprocessingmutex)

 

 




