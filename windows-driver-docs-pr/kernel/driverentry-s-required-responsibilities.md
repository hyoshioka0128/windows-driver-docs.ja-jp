---
title: DriverEntry の必要な責任
description: DriverEntry の必要な責任
ms.assetid: 6e997875-e7b7-43e2-8398-f0574f3a5816
keywords:
- DriverEntry WDK カーネル、必要な責任
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0adc60eb67d65e4c8b044ca005e7ef133fd984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838714"
---
# <a name="driverentrys-required-responsibilities"></a>DriverEntry の必要な責任





[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンの必須の順序付けられた責任は次のとおりです。

1.  ドライバーの標準ルーチンのエントリポイントを指定します。

    ドライバーは、標準ルーチンの多くについて、ドライバーオブジェクトまたはドライバーの拡張機能のエントリポイントを格納します。 このようなエントリポイントには、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン、ディスパッチルーチン、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチン、および[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン用のエントリポイントが含まれます。 たとえば、ドライバーは、 *AddDevice*、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、および[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンのエントリポイントを、次のようなステートメントで設定します (*Xxx*は、製造元が提供するドライバーを識別するプレフィックスのプレースホルダーです)。

    ```cpp
        :
    DriverObject->DriverExtension->AddDevice = XxxAddDevice;
    DriverObject->MajorFunction[IRP_MJ_PNP] = XxxDispatchPnp;
    DriverObject->MajorFunction[IRP_MJ_POWER] = XxxDispatchPower;
        :
    ```

    Isr や[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンなどの追加の標準ルーチンは、システムサポートルーチンを呼び出すことによって指定されます。 詳細については、個々の[標準ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)の説明を参照してください。

2.  ドライバーで使用するさまざまなドライバー全体のオブジェクト、型、またはリソースを作成または初期化します。 ほとんどの標準ルーチンでは、デバイスごとにオブジェクトが使用されるため、ドライバーでは、 *AddDevice*ルーチンでこのようなオブジェクトを設定するか、 [ **\_デバイス要求を開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)には、IRP\_を受け取った後に設定する必要があります。

    ドライバーがデバイス専用のスレッドを持っている場合、またはカーネル定義のディスパッチャーオブジェクトで待機している場合、 **Driverentry**ルーチンは[カーネルディスパッチャーオブジェクト](kernel-dispatcher-objects.md)を初期化する可能性があります。 (ドライバーがオブジェクトをどのように使用するかによって、 *AddDevice*ルーチンでこのタスクを実行したり、 **\_デバイス要求を開始\_IRP\_** を受け取った後に実行したりすることがあります)。

3.  割り当てられたすべてのメモリを解放し、不要になりました。

4.  ドライバーが正常に読み込まれたかどうかを示す NTSTATUS を返します。 PnP マネージャーからの要求を受け入れて処理し、デバイスの構成、追加、および起動を行うことができます。 ( [Driverentry の戻り値](driverentry-return-values.md)を参照してください。)

 

 




