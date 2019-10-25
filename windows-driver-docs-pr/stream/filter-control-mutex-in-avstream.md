---
title: AVStream のフィルター制御ミューテックス
description: AVStream のフィルター制御ミューテックス
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- フィルターコントロールミューテックス WDK AVStream
- AVStream ミューテックス WDK
- mutex WDK AVStream
- 同期 WDK AVStream
- 状態遷移 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 598698c94e317b226cc55729cb8d99a229d2f84f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834398"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream のフィルター制御ミューテックス





各 AVStream フィルターインスタンスには、関連付けられたフィルターコントロールミューテックスがあります。 この mutex は、フィルターから個々のピンまで、オブジェクト階層へのアクセスを同期するために使用されます。 フィルターとピンの作成と破棄は、この mutex と同期されます。

オブジェクト階層は、フィルターコントロールのミューテックスが保持されている間、特定のフィルターインスタンスから下方向に*のみ*安定していることが保証されます。 したがって、ミニドライバーは、**Ks***xxx***getfirstchild * * * xxx*関数および **ks***xxx***GetNextSibling * * * xxx*関数を使用して、フィルターレベルより下のオブジェクト階層を走査する前に、フィルターコントロールのミューテックスを取得する必要があります。

フィルターコントロールのミューテックスは、状態遷移の同期にも使用されます。

AVStream は、記述子の変更を実行するときなど、階層が安定している必要があるプロパティを処理するときに、フィルターコントロールのミューテックスを取得します。

個々のフィルターの下で、オブジェクト階層に1つのフィルターコントロールミューテックスが使用されていることに注意してください。 これは、ミニドライバーがピンオブジェクトを使用して関数を呼び出すときに、ピンオブジェクトが親のフィルターコントロールミューテックスを使用することを意味します。

AVStream は、次のミニドライバーが提供するルーチンを呼び出すときに、ミニドライバーに代わってフィルターコントロールのミューテックスを保持します。

-   [*AVStrMiniFilterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterirp)

-   [*AVStrMiniFilterClose*](https://docs.microsoft.com/previous-versions/ff556307(v=vs.85))

-   [*AVStrMiniPinCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinirp)

-   [*AVStrMiniPinClose*](https://docs.microsoft.com/previous-versions/ff556329(v=vs.85))

-   [*AVStrMiniPinConnect*](https://docs.microsoft.com/previous-versions/ff556332(v=vs.85))

-   [*AVStrMiniPinDisconnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinvoid)

-   [*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

-   [*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)

デバイスミューテックスと同様に、フィルターコントロールのミューテックスを再帰的に取得することはできません。 たとえば、AVStream が、スレッド A のコンテキストでの作成ディスパッチに対してミニドライバーへのコールバックを*作成*し、ミニドライバーが後でスレッド a からミューテックスを取得しようとすると、スレッド a がそれ自体とデッドロックします。

次のいずれかの操作を実行すると、デッドロックが発生する可能性があります。

-   プロセスルーチン内からフィルターコントロールミューテックスを取得してみてください。

-   スリープまたはウェイクコールバック内からフィルターコントロールミューテックスを取得します。

フィルターコントロールのミューテックスを操作するには、次の関数を使用します。

[**KsAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquirecontrol)、 [**KsFilterAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilteracquirecontrol)、 [**KsPinAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquirecontrol)、 [**KsReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasecontrol)、 [**KsFilterReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterreleasecontrol)、 [**KsPinReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinreleasecontrol)

 

 




