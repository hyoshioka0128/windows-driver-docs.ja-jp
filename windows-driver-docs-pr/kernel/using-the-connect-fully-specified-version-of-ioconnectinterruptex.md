---
title: IoConnectInterruptEx の CONNECT_FULLY_SPECIFIED バージョンの使用
description: IoConnectInterruptEx の CONNECT_FULLY_SPECIFIED バージョンの使用
ms.assetid: 5b75c32e-77e5-4761-b709-fedb8e33b57a
keywords:
- IoConnectInterruptEx
- CONNECT_FULLY_SPECIFIED
- 手動の割り込み検出 WDK カーネル
- 行ベースの割り込み WDK カーネル
- メッセージ シグナル割り込み WDK カーネル
- FullySpecified
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87ce7119c47166a0a70f02ec1f0f36f00e40b6b
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161462"
---
# <a name="using-the-connectfullyspecified-version-of-ioconnectinterruptex"></a>接続を使用して\_完全\_IoConnectInterruptEx の指定されたバージョン


ドライバーの接続を使用できる\_完全\_の指定されたバージョン[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)を登録する、 [ *InterruptService*](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチンの割り込みを特定します。 ドライバーの接続を使用できる\_完全\_指定されたバージョンの Windows Vista 以降します。 Iointex.lib ライブラリにリンクすると、ドライバーが接続を使用できます\_完全\_Windows 2000、Windows XP、および Windows Server 2003 で指定されたバージョン。 詳細については、次を参照してください。[を使用して IoConnectInterruptEx する前に Windows Vista](using-ioconnectinterruptex-prior-to-windows-vista.md)します。

ドライバーの接続の値を指定する\_完全\_に指定された*パラメーター * * *-&gt;バージョン** のメンバーを使用して*パラメーター * * *-&gt;FullySpecified** 操作の他のパラメーターを指定します。

-   *パラメーター * * *-&gt;FullySpecified.PhysicalDeviceObject** デバイスの PDO を指定する ISR サービス。

-   *パラメーター*-&gt;**FullySpecified.ServiceRoutine**を指す、 *InterruptService*中に、日常的な*パラメーター* - &gt; **FullySpecified**.**ServiceContext**として、システムが渡される値を指定します、 *ServiceContext*パラメーターを*InterruptService*します。 ドライバーは、コンテキスト情報を渡すためこれを使用できます。 コンテキスト情報を渡す方法についての詳細については、次を参照してください。 [ISR コンテキスト情報の提供](providing-isr-context-information.md)します。

-   ドライバーで PKINTERRUPT 変数へのポインターを提供します。 * パラメーター * **-&gt;FullySpecified.InterruptObject**します。 **IoConnectInterruptEx**ルーチンはできる割り込みの割り込みのオブジェクトをポイントするには、この変数を設定する際に使う[ISR を削除する](removing-an-isr.md)します。

-   ドライバーがでスピン ロックを必要に応じて指定*パラメーター * * *-&gt;FullySpecified.SpinLock** ISR との同期時に使用するシステム ほとんどのドライバーを指定するだけ**NULL**ドライバーに代わってスピン ロックの割り当てをシステムを有効にします。 ISR との同期の詳細については、次を参照してください。[デバイス データへのアクセスの同期](synchronizing-access-to-device-data.md)します。

ドライバーは、他のメンバーで、割り込みのキー プロパティを指定する必要があります * パラメーター * **-&gt;FullySpecified**します。 システムの配列に必要な情報を提供する[ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)構造体に送信するとき、 [**IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749) IRP がドライバーにします。

システムでは、各割り込みを**CM\_部分\_リソース\_記述子**構造体**型**メンバーに等しい**CmResourceTypeInterrupt**します。 メッセージ シグナル割り込みなど、CM の\_リソース\_割り込み\_のビットのメッセージ、**フラグ**メンバーのセットは、オフ、それ以外の場合。

**U.Interrupt**のメンバー **CM\_部分\_リソース\_記述子**行ベースの割り込みの説明を表すときに、 **u です。MessageInterrupt.Translated**メンバーには、メッセージ シグナル割り込みの説明が含まれています。 次の表で、場所を示します、 **CM\_部分\_リソース\_記述子**構造体のメンバーを設定するために必要な情報を検索する、 *パラメーター*- &gt; **FullySpecified**割り込みのどちらの種類。 詳細については、テーブルを次のコード例を参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>行ベースの割り込み</th>
<th>メッセージ シグナル割り込み</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ShareVector</strong></p></td>
<td><p><strong>ShareDisposition</strong></p></td>
<td><p><strong>ShareDisposition</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>ベクター</strong></p></td>
<td><p><strong>u.Interrupt.Vector</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Vector</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Irql</strong></p></td>
<td><p><strong>u.Interrupt.Level</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Level</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>InterruptMode</strong></p></td>
<td><p><strong>フラグ</strong>& CM_RESOURCE_INTERRUPT_LATCHED</p></td>
<td><p><strong>フラグ</strong>& CM_RESOURCE_INTERRUPT_LATCHED</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProcessorEnableMask</strong></p></td>
<td><p><strong>u.Interrupt.Affinity</strong></p></td>
<td><p><strong>u.MessageInterrupt.Translated.Affinity</strong></p></td>
</tr>
</tbody>
</table>

 

ドライバーは受信のみ**CM\_部分\_リソース\_記述子**メッセージ シグナル割り込み Windows Vista 以降のバージョンの Windows での構造体。

次のコード例は、登録する方法を示します、 *InterruptService*ルーチン CONNECT を使用して\_完全\_に指定します。

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

 

 




