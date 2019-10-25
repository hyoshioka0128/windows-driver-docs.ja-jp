---
title: IoConnectInterruptEx の CONNECT_FULLY_SPECIFIED バージョンの使用
description: IoConnectInterruptEx の CONNECT_FULLY_SPECIFIED バージョンの使用
ms.assetid: 5b75c32e-77e5-4761-b709-fedb8e33b57a
keywords:
- IoConnectInterruptEx
- CONNECT_FULLY_SPECIFIED
- 手動割り込み検出 WDK カーネル
- 行ベースの割り込み (WDK カーネル)
- メッセージシグナル割り込み (WDK カーネル)
- FullySpecified
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 770cd0c0c71ffc247c6c0fd06afffec49c8da7d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838334"
---
# <a name="using-the-connect_fully_specified-version-of-ioconnectinterruptex"></a>CONNECT\_を使用して、指定したバージョンの IoConnectInterruptEx を完全に\_する


ドライバーは、接続\_\_指定されたバージョンの[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を使用して、特定の割り込みの[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを登録できます。 ドライバーは、Windows Vista 以降で\_指定されたバージョンを完全に\_接続を使用できます。 ドライバーは、Iointex ライブラリにリンクすることにより、Windows 2000、Windows XP、および Windows Server 2003 で\_指定されたバージョンを完全に接続\_を使用できます。 詳細については、「 [Windows Vista より前の IoConnectInterruptEx の使用](using-ioconnectinterruptex-prior-to-windows-vista.md)」を参照してください。

ドライバーは、*パラメーター * * *-&gt;バージョン** に対して\_完全に指定された接続\_の値を指定し、*パラメーター * * *-&gt;FullySpecified** のメンバーを使用して操作の他のパラメーターを指定します。

-   *パラメーター * * *-&gt;FullySpecified PhysicalDeviceObject**、ISR がサービスを使用するデバイスの PDO を指定します。

-   *パラメーター-* &gt;**FullySpecified**は*InterruptService*ルーチンをポイントし、*パラメーター*は**FullySpecified**&gt;-ます。**ServiceContext**は、システムが*ServiceContext*パラメーターとして*InterruptService*に渡す値を指定します。 ドライバーはこれを使用してコンテキスト情報を渡すことができます。 コンテキスト情報を渡す方法の詳細については、「 [ISR コンテキスト情報の提供](providing-isr-context-information.md)」を参照してください。

-   ドライバーは、* Parameters * **-&gt;FullySpecified InterruptObject**の pkinterrupt 変数へのポインターを提供します。 **IoConnectInterruptEx**ルーチンは、この変数が、 [ISR を削除](removing-an-isr.md)するときに使用できる割り込みの interrupt オブジェクトを指すように設定します。

-   ドライバーでは、必要に応じて、*パラメーター * * *-&gt;FullySpecified** でスピンロックを指定できます。この場合、システムは ISR と同期するときに使用します。 ほとんどのドライバーでは、 **NULL**を指定するだけで、ドライバーの代わりにスピンロックを割り当てることができます。 ISR との同期の詳細については、「[デバイスデータへのアクセスの同期](synchronizing-access-to-device-data.md)」を参照してください。

ドライバーは、* Parameters * **-&gt;FullySpecified**の他のメンバーに割り込みのキープロパティを指定する必要があります。 システムは、 [ **\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)irp をドライバーに\_送信するときに、 [**CM\_PARTIAL\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体の配列に必要な情報を提供します。

システムは、 **CM\_部分\_リソース\_記述子**の構造体を、**型**のメンバーが**cmresourcetypeinterrupt**と等しくなるように提供します。 メッセージシグナル割り込みの場合は、CM\_リソース\_INTERRUPT\_メッセージビットの**Flags**メンバーが設定されます。それ以外の場合はクリアされます。

**CM\_部分\_リソース\_記述子**の**u. interrupt**メンバーには、行ベースの割り込みの説明が含まれてい**ます。** また、変換されたメンバーには、の説明が含まれています。メッセージシグナル割り込み。 次の表は、 **CM\_部分\_リソース\_記述子**構造体で **、&gt;-** *パラメーター*のメンバーを設定するために必要な情報を検索する場所を示しています。割り込みの種類。 詳細については、表の後に示すコード例を参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>行ベースの割り込み</th>
<th>メッセージシグナル割り込み</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>//ベクター</strong></p></td>
<td><p><strong>配置の破棄</strong></p></td>
<td><p><strong>配置の破棄</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>ベクトル</strong></p></td>
<td><p><strong>u. Interrupt. Vector</strong></p></td>
<td><p><strong>u. MessageInterrupt. Vector</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Irql</strong></p></td>
<td><p><strong>u. Interrupt. Level</strong></p></td>
<td><p><strong>u..... レベル</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>InterruptMode</strong></p></td>
<td><p><strong>フラグ</strong>& CM_RESOURCE_INTERRUPT_LATCHED</p></td>
<td><p><strong>フラグ</strong>& CM_RESOURCE_INTERRUPT_LATCHED</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProcessorEnableMask</strong></p></td>
<td><p><strong>u. Interrupt. Affinity</strong></p></td>
<td><p><strong>u.。変換された. Affinity</strong></p></td>
</tr>
</tbody>
</table>

 

ドライバーは、Windows Vista 以降のバージョンの Windows でメッセージシグナルが発生した割り込みに対して、 **CM\_部分的な\_リソース\_記述子**構造のみを受信します。

次のコード例は、CONNECT\_使用して、完全に\_指定された*InterruptService*ルーチンを登録する方法を示しています。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->IntObj is a PKINTERRUPT.
// deviceInterruptService is a pointer to the driver's InterruptService routine.
// IntResource is a CM_PARTIAL_RESOURCE_DESCRIPTOR structure of either type CmResourceTypeInterrupt or CmResourceTypeMessageInterrupt.
// PhysicalDeviceObject is a pointer to the device's PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_FULLY_SPECIFIED;
params.FullySpecified.PhysicalDeviceObject = PhysicalDeviceObject;
params.FullySpecified.InterruptObject = &devExt->IntObj;
params.FullySpecified.ServiceRoutine = deviceInterruptService;
params.FullySpecified.ServiceContext = ServiceContext;
params.FullySpecified.FloatingSave = FALSE;
params.FullySpecified.SpinLock = NULL;

if (IntResource->Flags & CM_RESOURCE_INTERRUPT_MESSAGE) {
    // The resource is for a message-signaled interrupt. Use the u.MessageInterrupt.Translated member of IntResource.
 
    params.FullySpecified.Vector = IntResource->u.MessageInterrupt.Translated.Vector;
    params.FullySpecified.Irql = (KIRQL)IntResource->u.MessageInterrupt.Translated.Level;
    params.FullySpecified.SynchronizeIrql = (KIRQL)IntResource->u.MessageInterrupt.Translated.Level;
    params.FullySpecified.ProcessorEnableMask = IntResource->u.MessageInterrupt.Translated.Affinity;
} else {
    // The resource is for a line-based interrupt. Use the u.Interrupt member of IntResource.
 
    params.FullySpecified.Vector = IntResource->u.Interrupt.Vector;
    params.FullySpecified.Irql = (KIRQL)IntResource->u.Interrupt.Level;
    params.FullySpecified.SynchronizeIrql = (KIRQL)IntResource->u.Interrupt.Level;
    params.FullySpecified.ProcessorEnableMask = IntResource->u.Interrupt.Affinity;
}

params.FullySpecified.InterruptMode = (IntResource->Flags & CM_RESOURCE_INTERRUPT_LATCHED ? Latched : LevelSensitive);
params.FullySpecified.ShareVector = (BOOLEAN)(IntResource->ShareDisposition == CmResourceShareShared);

status = IoConnectInterruptEx(&params);

if (!NT_SUCCESS(status)) {
    ...
}
```

 

 




