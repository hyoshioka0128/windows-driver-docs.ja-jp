---
title: AVStream のフィルター制御ミューテックス
description: AVStream のフィルター制御ミューテックス
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- コントロールのミュー テックス WDK AVStream をフィルター処理します。
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- WDK AVStream の同期
- 状態遷移 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4372cc34cb959dc3431b5c2fabc358eced0ee528
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384061"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream のフィルター制御ミューテックス





各 AVStream フィルター インスタンスには、関連付けられているフィルター コントロールのミュー テックスがあります。 このミュー テックスは、オブジェクト階層に個々 のピンにフィルターを下からのアクセスを同期に使用されます。 フィルターと pin の作成と破棄は、このミュー テックスと同期されます。

オブジェクト階層の安定したことが保証されて*のみ*フィルター コントロールの中に特定のフィルター インスタンスを下からミュー テックスが保持されています。 したがって、ミニドライバーは、フィルター レベルを使用して、以下のオブジェクト階層を移動する前のフィルター コントロール ミュー テックスを取得する必要があります、**Ks***Xxx***GetFirstChild * * * Xxx*と **Ks***Xxx***GetNextSibling * * * Xxx*関数。

フィルター コントロール ミュー テックスは、状態遷移の同期にも使用されます。

AVStream は、記述子の変更を実行するときなど、安定性を維持する階層を必要とするプロパティを処理する場合、フィルター コントロール ミュー テックスを取得します。

個々 のフィルターは各オブジェクトの階層に、1 つのフィルター コントロール ミュー テックスを使用することに注意します。 これは、ミニドライバーは、暗証番号 (pin) のオブジェクトの関数を呼び出すときに、暗証番号 (pin) のオブジェクトがその親のフィルター コントロール ミュー テックスを使用することを意味します。

AVStream は、次のミニドライバーが指定したルーチンを呼び出すときに、ミニドライバーに代わってフィルター コントロール ミュー テックスを保持します。

-   [*AVStrMiniFilterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterirp)

-   [*AVStrMiniFilterClose*](https://docs.microsoft.com/previous-versions/ff556307(v=vs.85))

-   [*AVStrMiniPinCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinirp)

-   [*AVStrMiniPinClose*](https://docs.microsoft.com/previous-versions/ff556329(v=vs.85))

-   [*AVStrMiniPinConnect*](https://docs.microsoft.com/previous-versions/ff556332(v=vs.85))

-   [*AVStrMiniPinDisconnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinvoid)

-   [*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdataformat)

-   [*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)

デバイス ミュー テックスと同様に、フィルター コントロール ミュー テックスいない取得する必要が再帰的にします。 かどうか、たとえば、AVStream に対してコールバックを実行、ミニドライバーの*作成*をそれ自体のスレッド A デッドロック、スレッド A 内からミュー テックスを取得しようとすると、スレッドのコンテキストで、ミニドライバー ディスパッチします。

アクションを次のいずれかの場合、デッドロックが発生することができます。

-   プロセス ルーチン内からフィルター コントロール ミュー テックスを取得しようとしてください。

-   スリープ状態またはスリープ解除コールバック内でいずれかからフィルター コントロール ミュー テックスを取得しようとしてください。

フィルター コントロール ミュー テックスを操作するには、次の関数を使用します。

[**KsAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquirecontrol)、 [ **KsFilterAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilteracquirecontrol)、 [ **KsPinAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinacquirecontrol)、 [**KsReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasecontrol)、 [ **KsFilterReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterreleasecontrol)、 [ **KsPinReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinreleasecontrol)

 

 




