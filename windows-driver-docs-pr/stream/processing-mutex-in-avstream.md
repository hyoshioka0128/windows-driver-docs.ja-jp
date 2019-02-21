---
title: AVStream でミュー テックスの処理
description: AVStream でミュー テックスの処理
ms.assetid: dd84fe3f-352e-4641-99d7-792ccecb0b40
keywords:
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- ミュー テックス WDK AVStream の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b731dfe3196ea56f645f37cda373cc711f8f7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553428"
---
# <a name="processing-mutex-in-avstream"></a>AVStream でミュー テックスの処理





3 番目のミュー テックスは、処理のミュー テックスです。 個別のフィルターと pin が独自の処理のミュー テックスがあります。 AVStream 独立していない処理ミュー テックスを獲得、フィルターと pin のレベルで処理する前に処理に関連する構造体へのアクセスを同期するためにします。 AVStream も処理ミュー テックスを獲得パイプ セクションへのピンのバインドを含むその他の操作中に、スリープ状態または電源の操作をスリープ解除し、記述子を変更します。 ミニドライバーは、処理操作または記述子の変更など、同期操作を実行するミュー テックスを取得手動でことができます。 変更の処理と同時に発生することはできませんが、前に、ミニドライバーは処理ミュー テックスを取得する必要があります。

など、他の 2 種類のミュー テックス、ミュー テックスの処理を再帰的には取得できません。 これは、ミニドライバーは、処理中に処理するミュー テックスを取得しようとする場合、デッドロックが発生したことを意味します。

長期間の処理を中断する処理のミュー テックスを使わないでください。 使用して直接処理制御ゲートを代わりに、操作、 **KSGATE * Xxx*** 関数。

スレッド処理のミュー テックスで取得した後でしようとしないでくださいフィルター コントロール ミュー テックスを取得します。

処理のミュー テックスを操作するには、次の関数を使用します。

[**KsFilterAcquireProcessingMutex**](https://msdn.microsoft.com/library/windows/hardware/ff562524)、 [ **KsPinAcquireProcessingMutex**](https://msdn.microsoft.com/library/windows/hardware/ff563488)、 [ **KsFilterReleaseProcessingMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff562552)、 [ **KsPinReleaseProcessingMutex**](https://msdn.microsoft.com/library/windows/hardware/ff563527)

 

 




