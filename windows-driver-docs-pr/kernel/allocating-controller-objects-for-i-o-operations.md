---
title: I/O 操作用のコントローラー オブジェクトの割り当て
description: I/O 操作用のコントローラー オブジェクトの割り当て
ms.assetid: 8a5e3741-f8ea-4e27-bb7f-6c20da1d618d
keywords:
- コント ローラー オブジェクトの WDK カーネルの割り当て
- ControllerControl ルーチン、コント ローラー オブジェクトの割り当て
- IoAllocateController
- コント ローラーのオブジェクトを割り当てください。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1d2b9aa7e305295ca8a226057d83e1b5f5aba9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369966"
---
# <a name="allocating-controller-objects-for-io-operations"></a>I/O 操作用のコントローラー オブジェクトの割り当て





コント ローラー オブジェクトを使用するドライバーがそのデバイスを起動した後、プロセス Irp がそのオブジェクトはターゲット デバイスに送信する準備が。 IRP が I/O 操作のコント ローラーのオブジェクトによって表される物理デバイスのプログラムにドライバーを必要とされるたびに、ドライバーが呼び出す[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)します。 次の図は、このような呼び出しを示しています。

![i/o コント ローラー オブジェクトの割り当てを示す図](images/3ctlaloc.png)

前の図に示すようにドライバーを指定する必要がありますよりも多く*ControllerObject*によって返されたポインター [ **IoCreateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller) 呼び出し時に[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)します。 このポインターと共に、ドライバーが提供する現在の I/O 要求の対象を表すデバイス オブジェクト、ポインターを渡す必要があります、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン、およびどのに*コンテキスト*その*ControllerControl*ルーチンは、要求された I/O 操作のデバイスを設定する必要があります。

**IoAllocateController**ドライバーによって提供されるキュー *ControllerControl*ルーチンの場合は、コント ローラー オブジェクトによって表されるデバイスがビジー状態です。 それ以外の場合、 *ControllerControl*ルーチンは、上記の図に示すように入力パラメーターを使用してすぐに呼び出されます。 入力*コンテキスト*へのポインター **IoAllocateController**ドライバーに渡される*ControllerControl*ルーチンを実行した場合。

コンテキスト情報を格納するのに場所を特定するのにには、次のガイドラインを使用します。

-   コント ローラー拡張機能で、ドライバーは、物理コント ローラーで別の操作を開始する前に完了するまで各 IRP を処理しない限り、ドライバーによって提供されるコンテキストの領域がすることはできません。 それ以外の場合、または新しい IRP の受信時にその他のドライバーのルーチンでコント ローラー拡張機能でコンテキストの領域は上書きされることができます。

-   ドライバーには、デバイス別のデバイス オブジェクトの I/O 操作が重なっていると、場合でも、ターゲット デバイス オブジェクトの拡張機能でデバイス コンテキストの領域を上書きできません。

-   特定のデバイス オブジェクトの別の I/O 要求が行われ、ドライバーは場合、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) 、日常的なデバイスの拡張機能内のコンテキストの領域も上書きできません受信 IRP があるため、ドライバーを呼び出すときにキューに置かれた[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)と同じ IRP はキューに残ります、デバイス ドライバー呼び出しまで[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)直前にそのデバイス オブジェクトの現在の IRP を完了します。

I/O マネージャーへのポインターを渡す、*デバイス オブジェクト*-&gt;**CurrentIrp**を*ControllerControl*ルーチンの場合、ドライバーは、 *StartIo*ルーチン。 かどうか、ドライバーは Irp の専用キューではなくを管理、 *StartIo* I/O マネージャーを与えることはできません、日常的な*ControllerControl*ルーチン現在 IRP へのポインター。 ドライバーを呼び出すと**IoAllocateController**、現在の IRP の一部として渡すか、*コンテキスト*-アクセス可能なデータ。

ドライバーのルーチンを呼び出す**IoAllocateController** IRQL で実行する必要があります = ディスパッチ\_レベルの呼び出しが発生した場合。 この呼び出しからは、ドライバー、 *StartIo*ルーチンがディスパッチで既に実行されている\_レベル。

*ControllerControl*ルーチンが IRP の要求された操作の物理的なコント ローラーを設定します。

前の図に示すように、 *ControllerControl*ルーチンは、型の値を返します[ **IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_io_allocation_action)、なることができます次のシステム定義の値のいずれか:

-   場合、 *ControllerControl*返すか、物理コント ローラーで別の操作を起動できるは、ルーチン、 **DeallocateObject**次に I/O 操作が要求されたため、ドライバーが重複することができます。

    たとえば場合、 *ControllerControl*ルーチンは、プログラムの 1 つのディスクのシーク操作のディスク コント ローラー、その IRP の完了、および戻り値**DeallocateObject**、 *ControllerControl*ルーチンは、転送要求は、他のディスクにキューが現在場合、その他のディスク上の転送操作のディスク コント ローラーをプログラムをもう一度呼び出すことができます。

-   現在の IRP では、その他のドライバー ルーチンでさらに処理が必要な場合、 *ControllerControl*ルーチンを返す必要があります**KeepObject**します。

    たとえば、ドライバーは、転送操作のディスク コント ローラーのプログラムが、転送が完了するまで、IRP を完了することはできません、 *ControllerControl*ルーチンを返す必要があります**KeepObject**します。

ときに、 *ControllerControl*ルーチンを返します**KeepObject**、デバイスが割り込み、ときに、ドライバーの ISR が通常実行し、その[ *DpcForIsr* 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチンでは、I/O 操作と対象のデバイス オブジェクトの現在の IRP が完了するとします。

たびに、 *ControllerControl*ルーチンを返します**KeepObject**、IRP を完了するルーチンを呼び出す必要があります[ **IoFreeController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller). このようなドライバーのルーチンを呼び出す必要があります**IoFreeController**次のデバイスの I/O 操作をすぐ設定できるように、できるだけ早くします。

 

 




