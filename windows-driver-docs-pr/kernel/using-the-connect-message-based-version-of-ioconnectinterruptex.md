---
title: IoConnectInterruptEx の CONNECT_MESSAGE_BASED バージョンを使用してください。
description: IoConnectInterruptEx の CONNECT_MESSAGE_BASED バージョンを使用してください。
ms.assetid: 8e06c6aa-85de-4ed2-ac0d-0179201d1272
keywords:
- IoConnectInterruptEx
- CONNECT_MESSAGE_BASED
- メッセージ シグナル割り込み WDK カーネル
- 割り込みを自動検出の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac0284c83bd60a376ec2a154d8526e72aa511c2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529981"
---
# <a name="using-the-connectmessagebased-version-of-ioconnectinterruptex"></a>接続を使用して\_メッセージ\_IoConnectInterruptEx のベース バージョン


Windows Vista 以降のオペレーティング システム、ドライバーが接続を使用できます\_メッセージ\_ベース バージョンの[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)のドライバーの ISR を登録するにはメッセージ シグナル割り込みです。 ドライバーの接続の値を指定する\_メッセージ\_に基づくの*パラメーター*-&gt;**バージョン**のメンバーを使用して*パラメーター*-&gt;**MessageBased**操作の他のパラメーターを指定します。

-   *パラメーター * * *-&gt;MessageBased.PhysicalDeviceObject** デバイスの PDO を指定する ISR サービス。 デバイス オブジェクトは、デバイスのメッセージ シグナル割り込みを自動的に識別するために使用されます。

-   *パラメーター * * *-&gt;MessageBased.MessageServiceRoutine** を指す、 [ *InterruptMessageService* ](https://msdn.microsoft.com/library/windows/hardware/ff547940)中に、日常的な*パラメーター * * *-&gt;MessageBased.ServiceContext** として、システムが渡される値を指定します、 *ServiceContext*パラメーターを*InterruptMessageService*します。 ドライバーは、コンテキスト情報を渡すためこれを使用できます。 コンテキスト情報を渡す方法についての詳細については、次を参照してください。 [ISR コンテキスト情報の提供](providing-isr-context-information.md)します。

-   ドライバーでは、フォールバックを指定できますも*InterruptMessageService*で日常的な*パラメーター ***-&gt;MessageBased.FallBackServiceRoutine**します。デバイスは、行ベースの割り込みがないメッセージ シグナル割り込みは、システムは登録代わりに、 *InterruptMessageService*行ベースの割り込みサービス ルーチン。この場合、システムに渡します*パラメーター * * *-&gt;MessageBased.ServiceContext** として、 *ServiceContext*パラメーターを[ *InterruptService*](https://msdn.microsoft.com/library/windows/hardware/ff547958)します。 **IoConnectInterruptEx**更新*パラメーター * * *-&gt;バージョン** connect\_行\_ベースのフォールバックのルーチンが登録されている場合。

-   *パラメーター * * *-&gt;MessageBased.ConnectionContext** をいずれかへのポインターを受け取る変数を指す、 [ **IO\_INTERRUPT\_メッセージ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550576) (の*InterruptMessageService*) 構造体または[ **KINTERRUPT** ](https://msdn.microsoft.com/library/windows/hardware/ff554237)構造 (の*InterruptService*). ドライバーは、受信したポインターを使用して ISR を削除することができます。 詳細については、次を参照してください。 [ISR を削除する](removing-an-isr.md)します。

-   ドライバーがでスピン ロックを必要に応じて指定*パラメーター * * *-&gt;MessageBased.SpinLock** ISR との同期時に使用するシステム ほとんどのドライバーを指定するだけ**NULL**ドライバーに代わってスピン ロックの割り当てをシステムを有効にします。 ISR との同期の詳細については、次を参照してください。[デバイス データへのアクセスの同期](synchronizing-access-to-device-data.md)します。

次のコード例は、登録する方法を示します、 *InterruptMessageService* CONNECT を使用して日常的な\_メッセージ\_ベース。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver&#39;s device extension. 
//     deviceExtension->IntInfo is a PVOID.
//     deviceExtension->IntType is a ULONG.
// deviceInterruptService is a pointer to the driver&#39;s InterruptService routine.
// deviceInterruptMessageService is a pointer to the driver&#39;s InterruptMessageService routine.
// PhysicalDeviceObject is a pointer to the device&#39;s PDO. 
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

 

 




