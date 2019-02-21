---
title: AVStream でコントロールのミュー テックスをフィルター処理します。
description: AVStream でコントロールのミュー テックスをフィルター処理します。
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- コントロールのミュー テックス WDK AVStream をフィルター処理します。
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- WDK AVStream の同期
- 状態遷移 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06a6af77bfa218d18fc6dab43c4f5c9b1d342d84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528761"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream でコントロールのミュー テックスをフィルター処理します。





各 AVStream フィルター インスタンスには、関連付けられているフィルター コントロールのミュー テックスがあります。 このミュー テックスは、オブジェクト階層に個々 のピンにフィルターを下からのアクセスを同期に使用されます。 フィルターと pin の作成と破棄は、このミュー テックスと同期されます。

オブジェクト階層の安定したことが保証されて*のみ*フィルター コントロールの中に特定のフィルター インスタンスを下からミュー テックスが保持されています。 したがって、ミニドライバーは、フィルター レベルを使用して、以下のオブジェクト階層を移動する前のフィルター コントロール ミュー テックスを取得する必要があります、**Ks***Xxx***GetFirstChild * * * Xxx*と **Ks***Xxx***GetNextSibling * * * Xxx*関数。

フィルター コントロール ミュー テックスは、状態遷移の同期にも使用されます。

AVStream は、記述子の変更を実行するときなど、安定性を維持する階層を必要とするプロパティを処理する場合、フィルター コントロール ミュー テックスを取得します。

個々 のフィルターは各オブジェクトの階層に、1 つのフィルター コントロール ミュー テックスを使用することに注意します。 これは、ミニドライバーは、暗証番号 (pin) のオブジェクトの関数を呼び出すときに、暗証番号 (pin) のオブジェクトがその親のフィルター コントロール ミュー テックスを使用することを意味します。

AVStream は、次のミニドライバーが指定したルーチンを呼び出すときに、ミニドライバーに代わってフィルター コントロール ミュー テックスを保持します。

-   [*AVStrMiniFilterCreate*](https://msdn.microsoft.com/library/windows/hardware/ff556310)

-   [*AVStrMiniFilterClose*](https://msdn.microsoft.com/library/windows/hardware/ff556307)

-   [*AVStrMiniPinCreate*](https://msdn.microsoft.com/library/windows/hardware/ff556334)

-   [*AVStrMiniPinClose*](https://msdn.microsoft.com/library/windows/hardware/ff556329)

-   [*AVStrMiniPinConnect*](https://msdn.microsoft.com/library/windows/hardware/ff556332)

-   [*AVStrMiniPinDisconnect*](https://msdn.microsoft.com/library/windows/hardware/ff556337)

-   [*AVStrMiniPinSetDataFormat*](https://msdn.microsoft.com/library/windows/hardware/ff556355)

-   [*AVStrMiniPinSetDeviceState*](https://msdn.microsoft.com/library/windows/hardware/ff556359)

デバイス ミュー テックスと同様に、フィルター コントロール ミュー テックスいない取得する必要が再帰的にします。 かどうか、たとえば、AVStream に対してコールバックを実行、ミニドライバーの*作成*をそれ自体のスレッド A デッドロック、スレッド A 内からミュー テックスを取得しようとすると、スレッドのコンテキストで、ミニドライバー ディスパッチします。

アクションを次のいずれかの場合、デッドロックが発生することができます。

-   プロセス ルーチン内からフィルター コントロール ミュー テックスを取得しようとしてください。

-   スリープ状態またはスリープ解除コールバック内でいずれかからフィルター コントロール ミュー テックスを取得しようとしてください。

フィルター コントロール ミュー テックスを操作するには、次の関数を使用します。

[**KsAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff560908)、 [ **KsFilterAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff562523)、 [ **KsPinAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff563485)、 [**KsReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff566780)、 [ **KsFilterReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff562551)、 [ **KsPinReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff563526)

 

 




