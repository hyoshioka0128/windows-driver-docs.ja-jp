---
title: ドライバーによって割り当てられたリソースの解放
description: ドライバーによって割り当てられたリソースの解放
ms.assetid: b286b4b0-54f2-4798-a77b-c08743502552
keywords:
- ルーチン WDK カーネルでは、非 PnP ドライバーをアンロードします。
- WDK カーネルの日常的な非 PnP アンロード
- ドライバーによって割り当てられたリソースを解放します。
- ドライバーによって割り当てられたリソースは、WDK のカーネルを解放します。
- リソースの解放 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578d93631f67edc7b566345d3eeda9f59db6b0d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373431"
---
# <a name="releasing-driver-allocated-resources"></a>ドライバーによって割り当てられたリソースの解放





ドライバーが、レジストリを使用する方法の詳細、システム オブジェクトとそのデバイスの拡張機能、コント ローラー拡張機能または非ページ プールのドライバーに割り当てられたリソースをセットでは、ドライバーが異なります。 ただし、すべて[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンは、段階的に、ドライバーを使用してリソースを解放する必要があります。

任意のドライバーの*アンロード*ルーチンする必要があることを確認しないその他のドライバーのルーチンが現在使用してすぐを使用して特定のリソースをそのリソースを解放する前にします。

一般に、*アンロード*ルーチンは、次の段階ですべてのドライバーに割り当てられたリソースを解放します。

1.  ドライバーが既に実行していない場合は、可能な場合、任意の物理デバイスの割り込みを無効にするを呼び出して[ **IoDisconnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)割り込みを無効にするようになります。

2.  その他のドライバーのルーチン参照できるようにしないリソースを*アンロード*ルーチンにリリースする予定です。

    たとえば、*アンロード*ルーチンを呼び出す必要があります[ **IoStopTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostoptimer)場合、ドライバーの[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンは特定のデバイス オブジェクトの現在有効です。 ドライバーのディスパッチャー オブジェクトのいずれかを待機しているスレッドがないへの呼び出しのキューにそのタイマー オブジェクトがないことが必ずその[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンの記憶域を解放する前に、ディスパッチャー オブジェクト。 呼び出す必要があります[ **KeRemoveQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovequeuedpc)がある場合、 [ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine) ISR がキューに置かれた可能性がありますが、ルーチンとします。

    ドライバーが呼び出された場合[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)、作業項目が完了していることを確認する必要があります。 **IoQueueWorkItem**は関連付けられているデバイス オブジェクトの参照を out; のような参照が残っている場合は、ドライバーをアンロードすることはできません。

    ドライバーが呼び出された場合[ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)、*アンロード*ルーチンもする必要がありますが発生する実行スレッド自体はを呼び出すことができるようにするドライバーが作成したスレッド[ **PsTerminateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psterminatesystemthread)ドライバーが読み込まれる前にします。 ドライバーは、呼び出すことによってシステムのドライバーが作成したスレッドを解放できません[ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)で、 *ThreadHandle*によって返される**PsCreateSystemThread**.

3.  ドライバーが割り当てられているデバイスに固有のリソースを解放します。 これにより、次のシステム サポート ルーチンを呼び出すことになる場合があります。
    -   [**IoDeleteSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletesymboliclink)場合、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)または[*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize) というルーチン[**IoCreateSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesymboliclink)または[ **IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreateunprotectedsymboliclink)、および[ **IoDeassignArcName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeassignarcname)ドライバーが呼び出された場合[ **IoAssignArcName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioassignarcname)します。

    -   [**ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)場合**DriverEntry**またはその他のルーチンのドライバーと呼ばれる[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)ドライバーがまだリリースされていないと割り当てられたメモリ。

    -   [**MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)します。

    -   [**MmFreeNonCachedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmfreenoncachedmemory)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmallocatenoncachedmemory).

    -   [**MmFreeContiguousMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreecontiguousmemory)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemory).

    -   [**FreeCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_common_buffer)場合、 **DriverEntry**または*を再初期化*というルーチン[ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer).

    -   [**IoAssignResources** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)または[ **IoReportResourceUsage** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)場合、 **DriverEntry**または*を再初期化*これらのルーチンと呼ばれる 1 サポート ルーチンまたは[ **HalAssignSlotResources** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))自体やその物理デバイスの構成のレジストリ内のハードウェア リソースを要求するには個別にします。

4.  システム オブジェクトとリソースを解放する、 **DriverEntry**または*を再初期化*ルーチンまたはコント ローラー オブジェクトのコント ローラー拡張機能にデバイス オブジェクトの拡張機能でデバイスを設定する (場合、作成されたいずれか)。 具体的には、ドライバーする必要があります、次の操作には、デバイス オブジェクトを削除する前に ([**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)) またはコント ローラーのオブジェクト ([**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeletecontroller)):
    -   呼び出す[ **IoDisconnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)対応するデバイスまたはコント ローラー拡張機能に格納されている割り込みオブジェクト ポインターを解放します。
    -   呼び出す[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)呼び出される場合に、次の下位ドライバーのファイル オブジェクトへのポインターが[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)デバイスまたはコント ローラーの拡張機能にこのポインターを格納します。
    -   呼び出す[ **IoDetachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)呼び出される場合、下位のドライバーのデバイス オブジェクトへのポインターが[ **IoAttachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevice)または[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)され、デバイスまたはコント ローラーの拡張機能にこのポインターを格納します。

5.  ハードウェア リソースを解放する、 **DriverEntry**または*を再初期化*ルーチンは、下のレジストリに存在する場合、ドライバーの物理デバイスでは、要求、 **\\レジストリ\\マシン\\ハードウェア\\ResourceMap**ツリー。

6.  そのデバイスのすべての名前を削除する、 **DriverEntry**または*を再初期化*ルーチンの下のレジストリに格納されている、 **\\レジストリ.\\DeviceMap**ツリーもします。

デバイス、システム、およびハードウェア リソースに、ドライバーがリリースされた後、次のセクションで説明した、デバイスとコント ローラーのオブジェクトを削除できます。

 

 




