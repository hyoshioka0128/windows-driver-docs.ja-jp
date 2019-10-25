---
title: CustomTimerDpc ルーチンの使用
description: CustomTimerDpc ルーチンの使用
ms.assetid: e95d01a2-4d13-40d2-aeb0-44c45e4a49f5
keywords:
- タイマーオブジェクト WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- タイマーオブジェクトの無効化
- タイマーオブジェクト WDK カーネル、無効化
- 定期的なタイマー WDK カーネル
- タイマーオブジェクトのキュー
- タイマーオブジェクト WDK カーネル、有効期限
- タイマーの有効期限 WDK カーネル
- 期限切れのタイマー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfaafb79eb94c50c34c2984847e0bad2855e7247
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838373"
---
# <a name="using-a-customtimerdpc-routine"></a>CustomTimerDpc ルーチンの使用





以前に設定したタイマーオブジェクトを無効にするために、ドライバーは[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)を呼び出します。 このルーチンは、システムのタイマーキューからタイマーオブジェクトを削除します。 一般に、タイマーオブジェクトはシグナル状態に設定されておらず、 *Customtimerdpc*ルーチンは実行のためにキューに登録されていません。 ただし、 **KeCancelTimer**が呼び出されたときにタイマーの有効期限が切れそうになると、 **KeCancelTimer**が時間キューにアクセスする前に有効期限が切れる可能性があります。この場合、シグナル通知および DPC キューが発生します。

以前に指定した*タイマー*と*Dpc*ポインターを使用した[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)または[**kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)の呼び出しは、前に指定した期間の有効期限が切れる前に、次のような影響を与えます。

-   カーネルは、オブジェクトをシグナル状態に設定したり、 *Customtimerdpc*ルーチンをキューに置いたりせずに、タイマーキューからタイマーオブジェクトを削除します。

-   新しい*DueTime*値を使用して、タイマーオブジェクトがタイマーキューに再挿入されます。

異なる目的で同じタイマーオブジェクトを使用すると、競合状態や重大なドライバーエラーが発生する可能性があります。 たとえば、 *Customtimerdpc*ルーチンの呼び出しを設定し、ドライバー専用のスレッドで待機を設定するために、1つのタイマーオブジェクトをドライバーが指定しているとします。 ドライバー専用のスレッドが、共通タイマーオブジェクトの**KeSetTimer**、 **kesettimerex**、または**KeCancelTimer**を呼び出すたびに、タイマーオブジェクトが既にキューに格納されていた場合、そのスレッドは*customtimerdpc*ルーチンへの呼び出しをキャンセルします。*Customtimerdpc*呼び出し。

ドライバーが*Customtimerdpc*ルーチンを持っていて、また、任意のスレッドコンテキストでタイマーオブジェクトを待機している場合は、次のことを行う必要があります。

-   スレッドコンテキストに依存しないタイマーオブジェクトは、任意のスレッドコンテキストでは使用しないでください。または、その逆も使用しないでください。

-   *Customtimerdpc*ルーチンごとに個別のタイマーオブジェクトを割り当てます。 任意のスレッドコンテキストで呼び出されるドライバースレッドまたはドライバールーチンの各セットには、独自の "待機可能な" タイマーオブジェクトのセットが含まれている必要があります。

*Customtimerdpc*ルーチンを使用する場合は、ドライバーが**KeSetTimer**または**kesettimerex**への呼び出しで渡す間隔を慎重に選択してください。 また、特に SMP プラットフォームでは、この呼び出しを行う任意のドライバールーチンと同じタイマーオブジェクトを使用して**KeCancelTimer**を呼び出すことによって発生する可能性のあるすべての影響を考慮してください。

*Customtimerdpc*ルーチンに関しては、次の点に注意してください。

特定の時点で実行するためにキューに入れることができるのは、特定の DPC ルーチンを表す DPC オブジェクトの1つだけです。

2番目のドライバールーチンが**KeSetTimer**または**Kesettimerex**を呼び出して、最初の呼び出し元によって指定された間隔の有効期限が切れる前に同じ*customtimerdpc*ルーチンを実行すると、 *customtimerdpc*ルーチンは間隔の後にのみ実行されます。2番目の呼び出し元で指定された有効期限が切れます。 このような状況では、 *Customtimerdpc*は、最初のルーチンが**KeSetTimer**または**kesettimerex**を呼び出した処理を実行しません。

*Customtimerdpc*ルーチンがあり、定期的なタイマーを使用するドライバーの場合:

ドライバーは、DPC ルーチンから定期的なタイマーの割り当てを解除することはできません。 ドライバーでは、DPC ルーチンからの非周期タイマーのみの割り当てを解除できます。

*Customdpc*と*customtimerdpc*ルーチンの両方を持つドライバーには、次の設計ガイドラインを考慮してください。

競合状態を防ぐため、 **KeSetTimer**または**Kesettimerex**と[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)に同じ*Dpc*ポインターを渡さないでください。

つまり、ドライバーの*StartIo*ルーチンが**KeSetTimer**または**Kesettimerex**を呼び出して*customtimerdpc*ルーチンをキューに登録し、ドライバーの ISR が別のプロセッサから同時に**KeInsertQueueDpc**を呼び出しているとします。同じ*Dpc*ポインター。 プロセッサ上の IRQL がディスパッチ\_レベルを下回るか、タイマー間隔が経過すると、その DPC ルーチンが実行されます。 どちらの方法を使用しても、 *StartIo*または ISR の重要な作業の一部が DPC ルーチンによって削除されるだけです。

さらに、機能が非常に異なる2つの標準ドライバールーチンで使用される DPC は、個別の*Customtimerdpc*と*customdpc*ルーチンよりもパフォーマンス特性が低下する可能性があります。 DPC は、 *StartIo*ルーチンまたは ISR によってキューに格納される原因に応じて、実行する操作を決定する必要があります。 DPC でこれらの条件をテストすると、追加の CPU サイクルが使用されます。

 

 




