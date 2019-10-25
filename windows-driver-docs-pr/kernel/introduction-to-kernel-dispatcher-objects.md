---
title: カーネル ディスパッチャー オブジェクトの概要
description: カーネル ディスパッチャー オブジェクトの概要
ms.assetid: acf7b19a-55a3-4d9b-87ff-ca4df9ed3a45
keywords:
- カーネルディスパッチャーオブジェクト WDK、カーネルディスパッチャーオブジェクトについて
- ディスパッチャーオブジェクト WDK カーネル、カーネルディスパッチャーオブジェクトについて
- 待機状態 WDK カーネル
- シグナル状態 WDK カーネル
- 非シグナル状態 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a0ee271e032de82e7c1e5fab3f55edbab7f704
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828201"
---
# <a name="introduction-to-kernel-dispatcher-objects"></a>カーネル ディスパッチャー オブジェクトの概要





カーネルは、*カーネルディスパッチャーオブジェクト*と呼ばれるオブジェクトの種類のセット、または*ディスパッチャーオブジェクト*を定義します。 ディスパッチャーオブジェクトには、タイマーオブジェクト、イベントオブジェクト、セマフォオブジェクト、ミューテックスオブジェクト、およびスレッドオブジェクトが含まれます。

ドライバーは、IRQL パッシブ\_レベルで実行しているときに、任意のスレッドコンテキスト内の同期メカニズムとしてディスパッチャーオブジェクトを使用できます。

### <a name="dispatcher-object-states"></a>ディスパッチャーオブジェクトの状態

すべてのカーネル定義ディスパッチャーオブジェクトの種類には、シグナル状態に設定される状態、または Not シグナル状態に設定されている状態があります。

スレッドのグループは、1つ以上のスレッドが[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)、 [**kewaitformutexobject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)、または[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)を呼び出した場合に、その操作を同期させることができます。 これらの関数は、ディスパッチャーオブジェクトポインターを入力として受け取り、別のルーチンまたはスレッドが1つ以上のディスパッチャーオブジェクトをシグナル状態に設定するまで待機します。

スレッドが、ディスパッチャーオブジェクト (またはミューテックスの**Kewaitformutexobject** ) を待機するために**KeWaitForSingleObject**を呼び出すと、ディスパッチャーオブジェクトがシグナル状態に設定されるまで、スレッドは*待機*状態になります。 スレッドは、 **KeWaitForMultipleObjects**を呼び出すことによって、すべてのディスパッチャーオブジェクトのセットがシグナル状態になるまで待機することができます。

ディスパッチャーオブジェクトがシグナル状態に設定されるたびに、カーネルはそのオブジェクトを待機しているスレッドの状態を*準備完了*に変更します。 (同期タイマーおよび同期イベントは、このルールの例外です。同期イベントまたはタイマーがシグナル状態になると、1つの待機中のスレッドのみが準備完了の状態に設定されます。 詳細については、「 [Timer オブジェクト」と「dpc](timer-objects-and-dpcs.md)と[イベントオブジェクト](event-objects.md)」を参照してください。)準備完了状態のスレッドは、現在の実行時の[スレッドの優先度](thread-priorities.md)に従って実行されるようにスケジュールされ、その優先順位を持つ任意のスレッドに対するプロセッサの現在の可用性を確保します。

### <a name="when-can-drivers-wait-for-dispatcher-objects"></a>ドライバーがディスパッチャーオブジェクトを待機できるようになるのはいつですか。

一般に、ドライバーは、次のいずれかの状況に該当する場合にのみ、ディスパッチャーオブジェクトが設定されるのを待機できます。

-   ドライバーは、任意のスレッドコンテキストで実行されていません。

    つまり、待機状態になるスレッドを識別できます。 実際には、任意のスレッドコンテキストで実行されるドライバールーチンは、任意のドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)、および[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンと、最上位レベルのドライバーのディスパッチルーチンだけです。 これらのルーチンはすべて、システムによって直接呼び出されます。

-   ドライバーは、完全に同期された i/o 要求を実行しています。

    つまり、i/o 要求の処理中にどのような操作もキューによって処理されることはなく、その下のドライバーが要求の処理を完了するまでドライバーは返されません。

また、ドライバーは、IRQL = ディスパッチ\_レベル以上で実行されている場合、待機状態になることはありません。

これらの制限に基づいて、次の規則を使用する必要があります。

-   ドライバーの**Driverentry**、 *AddDevice*、*再初期化*、および*アンロード*の各ルーチンは、ディスパッチャーオブジェクトを待機できます。

-   最上位レベルのドライバーのディスパッチルーチンは、ディスパッチャーオブジェクトを待機できます。

-   下位レベルのドライバーのディスパッチルーチンは、i/o 操作が同期されている場合 (作成、フラッシュ、シャットダウン、および閉じる操作、一部のデバイス i/o 制御操作、いくつかの PnP 操作と電源操作など)、ディスパッチオブジェクトを待機できます。

-   下位レベルのドライバーのディスパッチルーチンは、ディスパッチャーオブジェクトが非同期 i/o 操作の完了を待機することはできません。

-   IRQL ディスパッチ\_レベル以上で実行されているドライバールーチンは、ディスパッチャーオブジェクトがシグナル状態に設定されるのを待機することはできません。

-   ドライバーは、ページングデバイスとの間で転送操作を完了するために、ディスパッチャーオブジェクトがシグナル状態に設定されるのを待機することはできません。

-   読み取り/書き込み要求を処理するドライバーディスパッチルーチンは、通常、ディスパッチャーオブジェクトがシグナル状態に設定されるまで待機することはできません。

-   デバイス i/o 制御要求のディスパッチルーチンは、ディスパッチャーオブジェクトがシグナル状態になるのを待つことができます。これは、i/o 制御コードの転送の種類がメソッド\_バッファーに設定されている場合のみです。

-   SCSI ミニポートドライバーでは、カーネルディスパッチャーオブジェクトを使用しないでください。 SCSI ミニポートドライバーは、 [Scsi ポートライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のみを呼び出す必要があります。

他のすべての標準ドライバールーチンは、任意のスレッドコンテキストで実行されます。これは、キューに置かれた操作を処理したり、デバイスの割り込みを処理したりするためにドライバールーチンが呼び出されたときに、どのスレッドが最新であるかを示します。 また、ほとんどの標準的なドライバールーチンは、ディスパッチ\_レベル、または DIRQL のデバイスドライバーのいずれかで発生した IRQL で実行されます。

必要に応じて、ドライバーはデバイス専用のスレッドを作成できます。これは、ドライバーの他のルーチン (ISR または[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを除く) が、ディスパッチャーオブジェクトをシグナル状態に設定し、シグナル状態ではない状態にリセットするまで待機できます。

一般的なガイドラインとして、新しいデバイスドライバーが i/o 操作中にデバイスの状態の変化を待機している間に、50マイクロ秒を超えて停止することが予想される場合は、デバイス専用のスレッドを使用してドライバーを実装することを検討してください。 デバイスドライバーが最高レベルのドライバーでもある場合は、[システムワーカースレッド](system-worker-threads.md)を使用し、1つまたは複数のワーカースレッドコールバックルーチンを実装することを検討してください。 「 [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread) 」および「[ドライバーで作成されたスレッドを使用したインタロックキューの管理](managing-interlocked-queues-with-a-driver-created-thread.md)」を参照してください。

 

 




