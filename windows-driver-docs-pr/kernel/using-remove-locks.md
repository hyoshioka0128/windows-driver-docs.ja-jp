---
title: 削除ロックの使用
description: 削除ロックの使用
ms.assetid: 78ca7fe5-ceed-4752-bf1b-d13309097cd8
keywords:
- ロックの削除 WDK PnP
- ロックルーチン WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6376afa82412fb953b7cccfa71dafcb4280006a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835863"
---
# <a name="using-remove-locks"></a>削除ロックの使用





[Remove lock ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、デバイス上の未処理の i/o 操作の数を追跡し、ドライバーのデバイスオブジェクトをいつデタッチおよび削除できるかを判断するための手段を提供します。 システムは、独自の追跡機構を実装する代わりに、これらのルーチンをドライバーライターに提供します。

ドライバーは、次の2つの目的でこのメカニズムを使用できます。

1.  ドライバーの[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが IRP\_を完了しないようにするには、ロックが保持されている間 (別のドライバールーチンがデバイスにアクセスしているときなど) に\_デバイスの要求を[**削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)ます。

2.  ドライバーがデバイスオブジェクトを削除しない理由の数をカウントし、そのカウントがゼロになる場合にイベントを設定します。

削除ロックを初期化するには、ドライバーは、[デバイス拡張機能](device-extensions.md)で **\_ロック構造を削除\_IO**を割り当てる必要があります。その後、 [**Ioinitializer eremovelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)を呼び出します。 ドライバーは通常、デバイスオブジェクトの残りのデバイス拡張機能を初期化するときに、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで**Ioinitializer Eremovelock**を呼び出します。

ドライバーは、i/o 操作を開始するたびに[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出す必要があります。 ドライバーは、i/o 操作が完了するたびに[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出す必要があります。 ドライバーは、ロックを複数回取得できます。 Remove ロックルーチンは、ロックの未処理の取得の数を保持します。 **IoAcquireRemoveLock**を呼び出すたびにカウントが増加し、 **IoReleaseRemoveLock**はカウントをデクリメントします。

また、ドライバーのコード (タイマー、Dpc、コールバックなど) への参照を渡すときにも、 **IoAcquireRemoveLock**を呼び出す必要があります。 次に、ドライバーは、イベントが返されたときに**IoReleaseRemoveLock**を呼び出す必要があります。

IRP\_のディスパッチコードで[ **\_デバイス\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)する場合は、ドライバーがロックをもう一度取得してから、 [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出す必要があります。 このルーチンは、ロックの未処理のすべての取得が解放されるまでは戻りません。 キューに入っている i/o 操作が完了するのを許可するには、各ドライバーが IRP\_渡し*た後*、次のドライバーに\_デバイスの要求を**削除\_** 、その前に、その*前*に**IoReleaseRemoveLockAndWait**を呼び出す必要があります。メモリを解放するか、 [**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)を呼び出すか、 [**iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出します。 特定の remove ロックに対して**IoReleaseRemoveLockAndWait**が呼び出された後、同じ remove ロックに対する**IoAcquireRemoveLock**の後続の呼び出しはすべて失敗します。

**IoReleaseRemoveLockAndWait**が返された後、ドライバーはデバイスが削除可能な状態であると判断し、i/o 操作を実行できません。 そのため、ドライバーは、 **Ioinitializer Eremovelock**を呼び出して削除ロックを再初期化することはできません。 ドライバーが[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)によって検証されている間、この規則に違反すると、バグチェックが発生します。

ドライバーは、デバイスオブジェクトのデバイス拡張機能で **\_ロック構造を削除\_IO**を格納するため、\_\_IRP の処理中にドライバーがデバイス拡張機能を削除すると削除ロックが削除され **\_デバイス**の要求。

 

 




