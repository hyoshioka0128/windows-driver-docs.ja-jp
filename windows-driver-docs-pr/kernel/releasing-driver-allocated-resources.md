---
title: ドライバーによって割り当てられたリソースの解放
description: ドライバーによって割り当てられたリソースの解放
ms.assetid: b286b4b0-54f2-4798-a77b-c08743502552
keywords:
- アンロードルーチン WDK カーネル、非 PnP ドライバー
- PnP 以外のアンロードルーチン WDK カーネル
- ドライバーで割り当てられたリソースの解放
- ドライバーで割り当てられたリソースが WDK カーネルを解放する
- WDK カーネルを解放するリソース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc7d941d9c9fe7401e27291c61daa5739439169
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827462"
---
# <a name="releasing-driver-allocated-resources"></a>ドライバーによって割り当てられたリソースの解放





ドライバーがレジストリを使用する方法の詳細については、デバイス拡張機能、コントローラー拡張機能、またはドライバーによって割り当てられたページプールのシステムオブジェクトとリソースの設定は、ドライバーによって異なります。 ただし、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンでは、ドライバーが使用しているリソースを段階的に解放する必要があります。

ドライバーのすべての*アンロード*ルーチンは、そのリソースを解放する前に、他のドライバールーチンが現在使用していないか、特定のリソースをすぐに使用していることを確認する必要があります。

一般に、 *Unload*ルーチンは、次の段階でドライバーによって割り当てられたすべてのリソースを解放します。

1.  ドライバーがまだ実行していない場合は、可能であれば、任意の物理デバイスの割り込みを無効にしてから、割り込みが無効になるとすぐに[**Io切る割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)を呼び出します。

2.  *アンロード*ルーチンによってリリースされるリソースを他のドライバールーチンが参照できないことを確認します。

    たとえば、ドライバーの[*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンが特定のデバイスオブジェクトに対して現在有効になっている場合、 *Unload*ルーチンは[**iost最適化 er**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostoptimer)を呼び出す必要があります。 これにより、どのスレッドもドライバーのディスパッチャーオブジェクトを待機していないこと、およびそのタイマーオブジェクトが[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンへの呼び出しのためにキューに置かれていないことを確認してから、ディスパッチャーオブジェクトのストレージを解放する必要があります。 ISR がキューに登録されている可能性がある[*Customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンがある場合は、 [**KeRemoveQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovequeuedpc)を呼び出す必要があります。

    ドライバーが[**Ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)を呼び出した場合は、作業項目が完了していることを確認する必要があります。 **Ioqueueworkitem**は、関連付けられているデバイスオブジェクトの参照を取得します。このような参照が残っている場合は、ドライバーをアンロードできません。

    ドライバーが[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)を呼び出した場合、*アンロード*ルーチンは、ドライバーがアンロードされる前にスレッド自体が[**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread)を呼び出すことができるように、ドライバーによって作成されたスレッドを実行する必要もあります。 ドライバーは、 **PsCreateSystemThread**から返された*threadhandle*を使用して[**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出すことによって、ドライバーによって作成されたシステムスレッドを解放することはできません。

3.  ドライバーによって割り当てられたデバイス固有のリソースを解放します。 これを行うには、次のシステムサポートルーチンを呼び出す必要があります。
    -   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)または[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンが[**IoIoDeleteSymbolicLink YmIoCreateUnprotectedSymbolicLink iclink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)または[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)と呼ばれる場合は、 [**io**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink) [**arcname**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioassignarcname)というドライバーがある場合は[**iodeを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeassignarcname)関連付けます。

    -   **Driverentry**または[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)と呼ばれるその他のドライバールーチンが、割り当てられたメモリを解放していない場合は、 [**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 。

    -   **Driverentry**または*再初期化*ルーチンが[**mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)と呼ばれる場合は、 [**mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 。

    -   **Driverentry**または*再初期化*ルーチンが[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)という名前の場合、 [**MmFreeNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmfreenoncachedmemory) 。

    -   **Driverentry**または*再初期化*ルーチンが[**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)という名前の場合、 [**MmFreeContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory) 。

    -   **Driverentry**または*再初期化*ルーチンが[**allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)という名前の場合、 [**freecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_common_buffer) 。

    -   **Driverentry**または*再初期化*ルーチンがこれらのサポートルーチンまたは[**HalAssignSlotResources**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))のいずれかを呼び出して、構成レジストリ内のハードウェアリソース、またはその物理デバイスを個別に要求している場合は、 [**ioIoReportResourceUsage resources**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)または[](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl) 。

4.  **Driverentry**または*再初期化*ルーチンがデバイスオブジェクトのデバイス拡張機能またはコントローラーオブジェクトのコントローラー拡張機能 (作成されている場合) で設定したシステムオブジェクトとリソースを解放します。 特に、ドライバーは、デバイスオブジェクト ([**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)) またはコントローラーオブジェクト ([**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)) の削除を試みる前に、次の操作を行う必要があります。
    -   [**Io切る割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)を呼び出して、対応するデバイスまたはコントローラーの拡張機能に格納されている割り込みオブジェクトポインターを解放します。
    -   [**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)を呼び出し、デバイスまたはコントローラーの拡張機能にこのポインターを格納している場合は、次の下位にあるドライバーのファイルオブジェクトへのポインターを使用して[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出します。
    -   [**Ioattachdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)または[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出し、デバイスまたはコントローラーの拡張機能にこのポインターを格納している場合は、下位のドライバーのデバイスオブジェクトへのポインターを使用して[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)を呼び出します。

5.  ドライバーの物理デバイス (存在する場合) について、 **Driverentry**または*再初期化*のルーチンが要求したハードウェアリソースを解放します。これには、\\レジストリの下にあるレジストリ内の **\\マシン\\ハードウェア\\resourcemap**ツリー.

6.  **Driverentry**または*再初期化*ルーチンによってレジストリに格納されているデバイスの名前を、 **\\registry..\\DeviceMap**ツリーにも削除します。

ドライバーによってデバイス、システム、およびハードウェアリソースが解放された後、次のセクションで説明するように、デバイスとコントローラーオブジェクトを削除できます。

 

 




