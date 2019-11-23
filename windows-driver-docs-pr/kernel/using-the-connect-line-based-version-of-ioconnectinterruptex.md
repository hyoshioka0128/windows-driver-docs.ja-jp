---
title: IoConnectInterruptEx の CONNECT_LINE_BASED バージョンの使用
description: IoConnectInterruptEx の CONNECT_LINE_BASED バージョンの使用
ms.assetid: 245be266-f76c-43f6-9ea7-2dc853b1d5e2
keywords:
- IoConnectInterruptEx
- CONNECT_LINE_BASED
- 行ベースの割り込み (WDK カーネル)
- 自動割り込み検出 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b11f541600ce432672b4dedb569f1e2d8b42505
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835867"
---
# <a name="using-the-connect_line_based-version-of-ioconnectinterruptex"></a>IoConnectInterruptEx の接続\_行\_ベースバージョンの使用


Windows Vista 以降のオペレーティングシステムでは、ドライバーは、接続\_ライン\_ベースバージョンの[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を使用して、ドライバーのラインベースの割り込みに[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを登録できます。 (以前のオペレーティングシステムのドライバーでは、接続\_\_指定されたバージョンの**IoConnectInterruptEx**を完全に使用できます)。

この方法は、すべての行ベースの割り込みに対して1つの割り込みサービスルーチン (ISR) を登録するドライバーに対してのみ**使用   こと**ができます。 ドライバーが複数の割り込みを受信できる場合、指定されたバージョンの**IoConnectInterruptEx**\_完全に接続\_を使用する必要があります。

 

ドライバーは &gt;**バージョン**-*パラメーター*に基づいて接続\_行\_の値を指定し、*パラメーター*のメンバー-**linebased**を使用して操作の他のパラメーターを指定します。&gt;

-   *パラメーター*-&gt;**Linebased. PHYSICALDEVICEOBJECT**は、ISR がサービスを使用するデバイスの物理デバイスオブジェクト (PDO) を指定します。 システムは、デバイスオブジェクトを使用して、デバイスの回線ベースの割り込みを自動的に識別します。

-   *パラメーター*-&gt;**Lineeroutine**は*InterruptService*ルーチンをポイントしますが、*パラメーター*-&gt;**linebased**です。**ServiceContext**は、システムが*ServiceContext*パラメーターとして*InterruptService*に渡す値を指定します。 ドライバーはこれを使用してコンテキスト情報を渡すことができます。 コンテキスト情報を渡す方法の詳細については、「 [ISR コンテキスト情報の提供](providing-isr-context-information.md)」を参照してください。

-   ドライバーは、* Parameters * **-&gt;LineBased. InterruptObject**の pkinterrupt 変数へのポインターを提供します。 **IoConnectInterruptEx**は、この変数を割り込みの interrupt オブジェクトを指すように設定します。これは、ISR を削除するときに使用できます。 詳細については、「 [ISR の削除](removing-an-isr.md)」を参照してください。

-   ドライバーでは、必要に応じて、*パラメーター * * *-&gt;LineBased. スピン*ロックを指定できます。これは、システムが ISR と同期するときに使用します。 ほとんどのドライバーでは、 **NULL**を指定するだけで、ドライバーの代わりにスピンロックを割り当てることができます。 ISR との同期の詳細については、「[デバイスデータへのアクセスの同期](synchronizing-access-to-device-data.md)」を参照してください。

次のコード例は、CONNECT\_LINE\_を使用して*InterruptService*ルーチンを登録する方法を示しています。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntObj is a PKINTERRUPT.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_LINE_BASED;
params.LineBased.PhysicalDeviceObject = PhysicalDeviceObject;
params.LineBased.InterruptObject = &deviceExtension->IntObj;
params.LineBased.ServiceRoutine = deviceInterruptService;
params.LineBased.ServiceContext = ServiceContext;
params.LineBased.SpinLock = NULL;
params.LineBased.SynchronizeIrql = 0;
params.LineBased.FloatingSave = FALSE;

status = IoConnectInterruptEx(&params);

if (!NT_SUCCESS(status)) {
    // Operation failed. Handle error.
    ...
}
```

 

 




