---
title: I/O 操作用のコントローラー オブジェクトの割り当て
description: I/O 操作用のコントローラー オブジェクトの割り当て
ms.assetid: 8a5e3741-f8ea-4e27-bb7f-6c20da1d618d
keywords:
- コントローラーオブジェクト WDK カーネル、割り当て
- コントローラーオブジェクトの割り当てであるコントロールルーチン
- IoAllocateController
- コントローラーオブジェクトの割り当て
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cde992b60248b28a62a25e924c5c187753cc4d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828644"
---
# <a name="allocating-controller-objects-for-io-operations"></a>I/O 操作用のコントローラー オブジェクトの割り当て





コントローラーオブジェクトを使用するドライバーによってデバイスが起動されると、そのターゲットデバイスオブジェクトに送信される Irp を処理する準備が整います。 IRP で、i/o 操作のコントローラーオブジェクトによって表される物理デバイスをプログラムする必要がある場合、ドライバーは[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)を呼び出します。 次の図は、このような呼び出しを示しています。

![i/o のコントローラーオブジェクトの割り当てを示す図](images/3ctlaloc.png)

前の図に示されているように、ドライバーは[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)を呼び出すときに[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)によって返されたコントローラー以外の*オブジェクト*ポインターを指定する必要があります。 このポインターと共に、現在の i/o 要求のターゲットを表すデバイスオブジェクトへのポインター、ドライバーによって提供される[*コントローラー制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン、および*コントローラー*が必要とする*コンテキスト*を渡す必要があります。要求された i/o 操作のためにデバイスを設定します。

**IoAllocateController**は、コントローラーオブジェクトによって表されるデバイスがビジーである場合に、ドライバーによって提供される*コントロール*ルーチンをキューに置いています。 それ以外の場合は、前の図に示した入力パラメーターを使用して、*コントローラー制御*ルーチンが直ちに呼び出されます。 **IoAllocateController**への入力*コンテキスト*ポインターは、実行時にドライバーの*コントローラーの制御*ルーチンに渡されます。

コンテキスト情報を格納する場所を決定するには、次のガイドラインに従います。

-   ドライバーによって提供されるコンテキスト領域は、ドライバーが各 IRP を完了に処理した後、物理コントローラーで別の操作を開始するまでは、コントローラーの拡張機能に含まれないようにする必要があります。 それ以外の場合、コントローラー拡張機能内のコンテキスト領域は、他のドライバールーチンまたは新しい IRP の受信時に上書きされる可能性があります。

-   ドライバーが別のデバイスオブジェクトのデバイス i/o 操作と重複する場合でも、ターゲットデバイスオブジェクトのデバイス拡張機能のコンテキスト領域を上書きすることはできません。

-   特定のデバイスオブジェクトに対して別の i/o 要求が行われ、ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンがある場合、ドライバーが[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出したときに着信 IRP がキューに入れられるため、そのデバイス拡張機能のコンテキスト領域も上書きされません。同じ IRP がデバイスキューに保持されるのは、そのデバイスオブジェクトの現在の IRP を完了する直前に、ドライバーが[**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出すまでです。

ドライバーに*StartIo*ルーチンが含まれている場合、i/o マネージャーは、 *DeviceObject* **-&gt;のポインターを、** この*コントロール*ルーチンに渡します。 *StartIo*ルーチンを使わずに、ドライバーが irp の独自のキューを管理している場合、i/o マネージャーは、*コントローラー*に現在の IRP へのポインターを与えることはできません。 ドライバーが**IoAllocateController**を呼び出すと、*コンテキスト*にアクセスできるデータの一部として現在の IRP を渡す必要があります。

**IoAllocateController**を呼び出すドライバールーチンは、呼び出しが発生したときに、IRQL = ディスパッチ\_レベルで実行されている必要があります。 *StartIo*ルーチンからこの呼び出しを行うドライバーは、ディスパッチ\_レベルで既に実行されています。

コントローラー*制御*ルーチンは、IRP の要求された操作の物理コントローラーを設定します。

前の図に示されているように、*コントローラーの制御*ルーチンは、次のシステム定義の値のいずれかを使用して、 [**IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)の値を返します。

-   *コントローラーが*物理コントローラー上で別の操作を開始できる場合は、ドライバーが次に要求された i/o 操作と重複するように**Deallocateobject**を返す必要があります。

    たとえば、コントローラー*制御*ルーチンが1つのディスクでシーク操作のためにディスクコントローラーをプログラミングし、その IRP を完了して**Deallocateobject**を返すことができる場合、*コントロール*ルーチンを再び呼び出してディスクをプログラミングできます。他のディスクに対する転送操作のためのコントローラー。現在、転送要求が他のディスクのキューに格納されている場合。

-   現在の IRP が他のドライバールーチンによってさらに処理を必要とする場合、*コントローラーの制御*ルーチンは**KeepObject**を返す必要があります。

    たとえば、ドライブが転送操作のためにディスクコントローラーをプログラムするが、転送が完了するまで IRP を完了できない場合、*コントローラー制御*ルーチンは**KeepObject**を返す必要があります。

コントローラーの*制御*ルーチンが**KeepObject**を返すと、通常、ドライバーの ISR はデバイスの割り込み時に実行され、その[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、ターゲットデバイスの i/o 操作と現在の IRP を完了します。素材.

コントローラーの*制御*ルーチンが**KeepObject**を返すたびに、IRP を完了するルーチンは[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)を呼び出す必要があります。 このようなドライバールーチンは、次のデバイス i/o 操作をすぐに設定できるように、できるだけ早く**IoFreeController**を呼び出す必要があります。

 

 




