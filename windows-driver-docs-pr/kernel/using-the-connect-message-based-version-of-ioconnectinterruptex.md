---
title: IoConnectInterruptEx の CONNECT_MESSAGE_BASED バージョンの使用
description: IoConnectInterruptEx の CONNECT_MESSAGE_BASED バージョンの使用
ms.assetid: 8e06c6aa-85de-4ed2-ac0d-0179201d1272
keywords:
- IoConnectInterruptEx
- CONNECT_MESSAGE_BASED
- メッセージシグナル割り込み (WDK カーネル)
- 自動割り込み検出 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b243220efad966ef8d1964fe5d727d3c13c5ffb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838331"
---
# <a name="using-the-connect_message_based-version-of-ioconnectinterruptex"></a>CONNECT\_MESSAGE\_BASED バージョンの IoConnectInterruptEx を使用する


Windows Vista 以降のオペレーティングシステムでは、ドライバーは、接続\_メッセージ\_ベースバージョンの[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を使用して、ドライバーのメッセージシグナル割り込みに ISR を登録できます。 ドライバーは&gt;**バージョン**-*パラメーター*に基づいて CONNECT\_MESSAGE\_の値を指定し、*パラメーター*のメンバー-**messagebased**を使用して他のパラメーターを指定します。操作の。&gt;

-   *パラメーター * * *-&gt;MessageBased. PhysicalDeviceObject**、ISR がサービスを使用するデバイスの PDO を指定します。 システムは、デバイスオブジェクトを使用して、デバイスのメッセージシグナル割り込みを自動的に識別します。

-   *パラメーター * * *-&gt;MessageBased. MessageServiceRoutine** は[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)ルーチンをポイントしますが、*パラメーター * * *-&gt;messagebased. ServiceContext** は、システムによって渡される値を*ServiceContext*パラメーターを*InterruptMessageService*に指定します。 ドライバーはこれを使用してコンテキスト情報を渡すことができます。 コンテキスト情報を渡す方法の詳細については、「 [ISR コンテキスト情報の提供](providing-isr-context-information.md)」を参照してください。

-   ドライバーでは、 *パラメーター * **-&gt;Messagebased. FallBackServiceRoutine**でフォールバック InterruptMessageService ルーチンを指定することもできます。デバイスに行ベースの割り込みがあるにもかかわらず、メッセージシグナルの割り込みがない場合は、行ベースの割り込みを処理するために*InterruptMessageService*ルーチンが登録されます。この場合、システムは*パラメーター * * *-&gt;**  *ServiceContext*パラメーターとして[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)に渡します。 **IoConnectInterruptEx**は、*パラメーター * * *-&gt;Version** を更新して、フォールバックルーチンが登録されているかどうかに基づいて\_行\_を接続します。

-   *Parameters * * *-&gt;MessageBased. ConnectionContext** は、 [**IO\_割り込み\_MESSAGE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info) ( *InterruptMessageService*) 構造体また[**はのいずれかへのポインターを受け取る変数を指します。KINTERRUPT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体 ( *InterruptService*の場合)。 ドライバーは、受信したポインターを使用して ISR を削除できます。 詳細については、「 [ISR の削除](removing-an-isr.md)」を参照してください。

-   ドライバーでは、必要に応じて、*パラメーター * * *-&gt;MessageBased. スピン*ロックを指定できます。これは、システムが ISR と同期するときに使用します。 ほとんどのドライバーでは、 **NULL**を指定するだけで、ドライバーの代わりにスピンロックを割り当てることができます。 ISR との同期の詳細については、「[デバイスデータへのアクセスの同期](synchronizing-access-to-device-data.md)」を参照してください。

次のコード例は、CONNECT\_MESSAGE\_BASED を使用して、 *InterruptMessageService*ルーチンを登録する方法を示しています。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntInfo is a PVOID.
//     deviceExtension->IntType is a ULONG.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// deviceInterruptMessageService is a pointer to the driver's InterruptMessageService routine.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;
params.MessageBased.PhysicalDeviceObject = PhysicalDeviceObject;
params.MessageBased.MessageServiceRoutine = deviceInterruptMessageService;
params.MessageBased.ServiceContext = ServiceContext;
params.MessageBased.SpinLock = NULL;
params.MessageBased.SynchronizeIrql = 0;
params.MessageBased.FloatingSave = FALSE;
params.MessageBased.FallBackServiceRoutine = deviceInterruptService;

status = IoConnectInterruptEx(&params);

if (NT_SUCCESS(status)) {
    // We record the type of ISR registered.
    devExt->IsrType = params.Version;
} else {
    // Operation failed. Handle error.
    ...
}
```

 

 




