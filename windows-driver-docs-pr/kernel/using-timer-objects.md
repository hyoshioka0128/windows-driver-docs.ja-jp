---
title: タイマー オブジェクトの使用
description: タイマー オブジェクトの使用
ms.assetid: b3ee9d92-87b9-47b7-ab13-11e42bec7997
keywords:
- タイマーオブジェクト WDK カーネル、待機中
- タイマーオブジェクトを待機しています
- 通知タイマー WDK カーネル
- KeDelayExecutionThread
- KeWaitForSingleObject
- KeInitializeTimer
- KeSetTimer
- DueTime の値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5297b5703b0424d3b7f348313f0fb57151ee9eeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835843"
---
# <a name="using-timer-objects"></a>タイマー オブジェクトの使用





次の図は、通知タイマーを使用して操作のタイムアウト間隔を設定し、他のドライバールーチンが i/o 要求を処理している間待機する方法を示しています。

![タイマーオブジェクトを待機していることを示す図](images/3ketimer.png)

前の図に示すように、ドライバーは、このストレージへのポインターを使用して[**Keinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)への呼び出しで初期化する必要があるタイマーオブジェクト用のストレージを提供する必要があります。 ドライバーは、通常、この呼び出しを[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンから行います。

ドライバーによって作成されたスレッドや、同期 i/o 操作を要求するスレッドなど、特定のスレッドのコンテキスト内では、前の図に示すように、ドライバーはタイマーオブジェクトを待機できます。

1.  スレッドは、タイマーオブジェクトへのポインターと、100ナノ秒単位で表される特定の*DueTime*値を使用して、 [**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)を呼び出します。 *DueTime*の正の値は、タイマーオブジェクトをカーネルのタイマーキューから削除し、シグナル状態に設定する絶対時刻を指定します。 *DueTime*の負の値は、現在のシステム時刻を基準とする間隔を指定します。

    スレッド (またはシステムスレッドで実行されているドライバールーチン) が、 **KeSetTimer**を呼び出すときに、dpc オブジェクト (または[customtimerdpc ルーチンではタイマーと dpc オブジェクトを使用する方法](registering-and-queuing-a-customtimerdpc-routine.md)を示す図で前述) に対して**NULL**ポインターを渡すことに注意してください。[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンをキューに入れずにタイマーオブジェクトを待機する場合はです。

2.  スレッドは、タイマーオブジェクトへのポインターを使用して[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出します。これにより、タイマーオブジェクトがカーネルのタイマーキューに格納されている間、スレッドが待機状態になります。

3.  指定された*DueTime*の有効期限が切れます。

4.  カーネルは timer オブジェクトをデキューし、シグナル状態に設定して、スレッドの状態を [待機中] から [準備完了] に変更します。

5.  カーネルは、プロセッサが使用可能になるとすぐにスレッドをディスパッチします。つまり、優先度の高い他のスレッドは現在準備完了状態であり、カーネルモードルーチンが上位の IRQL で実行されることはありません。

IRQL &gt;= DISPATCH\_レベルで実行されるドライバールーチンでは、タイマーオブジェクトと関連する DPC オブジェクトを使用して、ドライバーによって提供される[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンをキューに置いて、要求をタイムアウトさせることができます。 任意のスレッドコンテキスト内で実行されるドライバールーチンだけが、前の図に示すように、タイマーオブジェクトに対して0以外の間隔を待機できます。

他のすべてのスレッドと同様に、ドライバーで作成されたスレッドは、ディスパッチャーオブジェクトでもあるカーネルスレッドオブジェクトによって表されます。 そのため、ドライバーでは、ドライバーによって作成されたスレッドを使用する必要はありません。タイマーオブジェクトを使用して、特定の間隔で自発的に待機状態にする必要があります。 代わりに、スレッドは、呼び出し元が指定した間隔で[**Kedelayexecutionthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)を呼び出すことができます。 この手法の詳細については、「[デバイスのポーリング](avoid-polling-devices.md)」を参照してください。

[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)、および[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンもシステムスレッドコンテキストで実行されるため、ドライバーが初期化されたタイマーオブジェクトまたは**kedelayexecutionthread**を使用しているときに、ドライバーが**KeWaitForSingleObject**を呼び出すことができます。初期化中またはアンロード中です。 デバイスドライバーは、初期化中にデバイスが状態を更新するのを待機する必要がある場合、非常に短い間隔 (できれば50マイクロ秒未満) に[**Kestallexecutionprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)を呼び出すことができます。

ただし、高レベルのドライバーでは、通常、タイマーオブジェクトを使用する代わりに、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)と[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンで別の同期メカニズムを使用します。 上位レベルのドライバーは、特定の種類または種類のデバイスの下位レベルのドライバーに対して常にレイヤーを作成するように設計する必要があります。 そのため、より高いレベルのドライバーは、タイマーオブジェクトを待機している場合、または**Kedelayexecutionthread**を呼び出す場合、読み込みに時間がかかる傾向があります。このようなドライバーは、それをサポートしている最も低速なデバイスを格納するのに十分な期間待機する必要があるためです。 また、このような待機では、"安全" だが、最短の間隔を決定するのは非常に難しいことに注意してください。

同様に、PnP ドライバーは他のアクションが発生するのを待たずに、代わりに PnP マネージャーの[通知](using-pnp-notification.md)メカニズムを使用する必要があります。

 

 




