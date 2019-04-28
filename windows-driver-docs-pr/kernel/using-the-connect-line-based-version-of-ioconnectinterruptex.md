---
title: IoConnectInterruptEx の CONNECT_LINE_BASED バージョンの使用
description: IoConnectInterruptEx の CONNECT_LINE_BASED バージョンの使用
ms.assetid: 245be266-f76c-43f6-9ea7-2dc853b1d5e2
keywords:
- IoConnectInterruptEx
- CONNECT_LINE_BASED
- 行ベースの割り込み WDK カーネル
- 割り込みを自動検出の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e6492af31d6485d56810df9f51b18014de61ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372306"
---
# <a name="using-the-connectlinebased-version-of-ioconnectinterruptex"></a>接続を使用して\_行\_IoConnectInterruptEx のベース バージョン


Windows Vista 以降のオペレーティング システム、ドライバーが接続を使用できます\_行\_ベース バージョンの[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)を登録する、 [ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)行ベースのドライバーの割り込みのルーチンです。 (以前のオペレーティング システム用のドライバーの接続を使用できる\_完全\_の指定されたバージョン**IoConnectInterruptEx**)。

**注**  すべての行ベースの割り込みの 1 つの割り込みサービス ルーチン (ISR) を登録するドライバーに対してだけ、このメソッドを使用することができます。 接続を使用する必要があります、ドライバーは、複数の割り込みを受け取ることが場合、\_完全\_の指定されたバージョン**IoConnectInterruptEx**します。

 

ドライバーの接続の値を指定する\_行\_に基づくの*パラメーター*-&gt;**バージョン**のメンバーを使用して*パラメーター*-&gt;**LineBased**操作の他のパラメーターを指定します。

-   *パラメーター*-&gt;**LineBased.PhysicalDeviceObject**デバイスの物理デバイス オブジェクト (PDO) を指定する ISR サービス。 デバイス オブジェクトは、行ベースのデバイスの割り込みを自動的に識別するために使用されます。

-   *パラメーター*-&gt;**LineBased.ServiceRoutine**を指す、 *InterruptService*中に、日常的な*パラメーター*- &gt; **LineBased**.**ServiceContext**として、システムが渡される値を指定します、 *ServiceContext*パラメーターを*InterruptService*します。 ドライバーは、コンテキスト情報を渡すためこれを使用できます。 コンテキスト情報を渡す方法についての詳細については、次を参照してください。 [ISR コンテキスト情報の提供](providing-isr-context-information.md)します。

-   ドライバーで PKINTERRUPT 変数へのポインターを提供します。 * パラメーター ***-&gt;LineBased.InterruptObject**します。 **IoConnectInterruptEx** ISR を削除するときに使用できると、割り込みの割り込みのオブジェクト をポイントするには、この変数を設定 詳細については、次を参照してください。 [ISR を削除する](removing-an-isr.md)します。

-   ドライバーがでスピン ロックを必要に応じて指定*パラメーター * * *-&gt;LineBased.SpinLock** ISR との同期時に使用するシステム ほとんどのドライバーを指定するだけ**NULL**ドライバーに代わってスピン ロックの割り当てをシステムを有効にします。 ISR との同期の詳細については、次を参照してください。[デバイス データへのアクセスの同期](synchronizing-access-to-device-data.md)します。

次のコード例は、登録する方法を示します、 *InterruptService* CONNECT を使用してルーチン\_行\_ベース。

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

 

 




