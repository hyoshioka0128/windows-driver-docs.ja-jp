---
title: Active-Both 割り込みの処理
description: Active-Both 割り込みの処理
ms.assetid: CFA205B1-FDDD-4E27-8CF9-106C8D1CC4EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66568a41b18d1e9599cb199b24721259ccbb932f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844431"
---
# <a name="handling-active-both-interrupts"></a>Active-Both 割り込みの処理


**注**  このトピックは、カーネルモードドライバーフレームワーク (kmdf) バージョン1.13 以前にのみ適用されます。

 

多くのデバイスには、割り込みの生成とマスキングを制御するハードウェアレジスタがあります。 通常、このようなデバイスの KMDF および UMDF ドライバーは、フレームワークの組み込みの割り込みサポートを使用します。

ただし、チップ (SoC) ハードウェアプラットフォーム上のシステム上の単純なデバイスには、割り込み用のハードウェアレジスタがない場合があります。 その結果、割り込みが生成されるタイミングを制御できない場合や、ハードウェアで割り込みをマスクできる場合があります。 デバイスが接続時にすぐに割り込み、ドライバーがフレームワークの割り込みサポートを使用している場合は、フレームワークがフレームワークの interrupt オブジェクトを完全に初期化する前に割り込みが発生する可能性があります。 その結果、KMDF ドライバーは、接続して割り込みを切断するために、WDM ルーチンを直接呼び出す必要があります。 UMDF ドライバーはこれらのメソッドを呼び出すことができないため、このようなデバイスには UMDF ドライバーを書き込むことはできません。

このトピックでは、KMDF ドライバーがこのようなデバイスの割り込みを処理する方法について説明します。

SoC ハードウェアプラットフォームでは、アクティブ-両方の割り込みは通常、ハードウェアプッシュボタンなどの非常に単純なデバイスに使用されます。 ユーザーがプッシュボタンを押すと、デバイスの割り込み信号線が低から高に、または高から低に遷移します。 ユーザーがプッシュボタンを放すと、割り込み線は反対方向に遷移します。 アクティブ-両方の割り込み入力として構成された GPIO pin は、低対高の遷移と高対低の遷移の両方で割り込みを生成するため、システムは両方の場合に周辺機器ドライバーの割り込みサービスルーチン (ISR) を呼び出します。 ただし、ドライバーは、移行が低対高または高から低のどちらであるかを示すものではありません。

低い遷移と高対低の遷移を区別するために、ドライバーは各割り込みの状態を追跡する必要があります。 これを行うために、ドライバーでは、割り込みラインの状態が低い場合は**FALSE**であり、行の状態が高の場合は**TRUE**になるブール値の割り込み状態の値を維持することができます。

システムの起動時に行の状態が既定値 low になる例を考えてみましょう。 このドライバーは、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で状態値を**FALSE**に初期化します。 その後、ドライバーの ISR が呼び出されるたびに、状態の変化が通知されます。その後、ドライバーはその ISR の状態値を反転します。

システムの起動時に行の状態が高い場合は、有効になった直後に割り込みが発生します。 ドライバーは、 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンを直接呼び出すのではなく、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出すのではなく、直ちに可能な割り込みを受け取ることを保証します。

このソリューションでは、GPIO コントローラーがハードウェアのアクティブな割り込みをサポートするか、または GPIO コントローラーのドライバーがソフトウェアのアクティブな割り込みをエミュレートする必要があります。 アクティブな両方の割り込みをエミュレートする方法の詳細については、[**コントローラー\_属性\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_controller_attribute_flags)構造体の**EmulateActiveBoth**メンバーの説明を参照してください。

次のコード例は、周辺機器の KMDF ドライバーが割り込み極性を追跡する方法を示しています。

```cpp
typedef struct _INTERRUPT_CONTEXT INTERRUPT_CONTEXT, *PINTERRUPT_CONTEXT;
typedef struct _DEVICE_CONTEXT DEVICE_CONTEXT, *PDEVICE_CONTEXT;


struct _INTERRUPT_CONTEXT
{
               BOOLEAN State;
               PDEVICE_CONTEXT DeviceContext;
};

struct _DEVICE_CONTEXT
{
               PKINTERRUPT Interrupt;
               INTERRUPT_CONTEXT InterruptContext;
               PDEVICE_OBJECT PhysicalDeviceObject;
               KSPIN_LOCK SpinLock;
};

...

BOOLEAN
YourInterruptIsr(
               __in PKINTERRUPT Interrupt,
               __in PVOID ServiceContext
               )
{
               PINTERRUPT_CONTEXT InterruptContext = (PINTERRUPT_CONTEXT)ServiceContext;
               PDEVICE_CONTEXT DeviceContext = InterruptContext->DeviceContext;

               //
               // Flip the state.
               //
               InterruptContext->State = !InterruptContext->State;

               IoRequestDpc(DeviceContext->PhysicalDeviceObject, DeviceContext->PhysicalDeviceObject->CurrentIrp, InterruptContext);
}

VOID
YourInterruptDpc(
               __in PKDPC Dpc,
               __in PDEVICE_OBJECT DeviceObject,
               __inout PIRP Irp,
               __in_opt PVOID ContextPointer
               )
{
               PINTERRUPT_CONTEXT InterruptContext = (PINTERRUPT_CONTEXT)ContextPointer;

               ...
}

NTSTATUS
EvtDriverDeviceAdd(
               __in  WDFDRIVER Driver,
               __in  PWDFDEVICE_INIT DeviceInit
               )
{
               WDFDEVICE Device;
               PDEVICE_CONTEXT DeviceContext;

               ...

               DeviceContext->Interrupt = NULL;
               DeviceContext->PhysicalDeviceObject = WdfDeviceWdmGetPhysicalDevice(Device);
               KeInitializeSpinLock(&DeviceContext->SpinLock);

               IoInitializeDpcRequest(DeviceContext->PhysicalDeviceObject, YourInterruptDpc);
}

NTSTATUS
EvtDevicePrepareHardware(
               __in  WDFDEVICE Device,
               __in  WDFCMRESLIST ResourcesRaw,
               __in  WDFCMRESLIST ResourcesTranslated
               )
{
               PDEVICE_CONTEXT DeviceContext = YourGetDeviceContext(Device);

               for (ULONG i = 0; i < WdfCmResourceListGetCount(ResourcesTranslated); i++)
               {
                              PCM_PARTIAL_RESOURCE_DESCRIPTOR descriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, i);

                              if (descriptor->Type == CmResourceTypeInterrupt)
                              {
                                             IO_CONNECT_INTERRUPT_PARAMETERS params;
                                             RtlZeroMemory(&params, sizeof(params));

                                             params.Version = CONNECT_FULLY_SPECIFIED;
                                             params.FullySpecified.PhysicalDeviceObject = DeviceContext->PhysicalDeviceObject;
                                             params.FullySpecified.InterruptObject = &DeviceContext->Interrupt;
                                             params.FullySpecified.ServiceRoutine = YourInterruptIsr;
                                             params.FullySpecified.ServiceContext = (PVOID)&DeviceContext->InterruptContext;
                                             params.FullySpecified.SpinLock = &DeviceContext->SpinLock;
                                             params.FullySpecified.Vector = descriptor->u.Interrupt.Vector;
                                             params.FullySpecified.Irql = (KIRQL)descriptor->u.Interrupt.Level;
                                             params.FullySpecified.SynchronizeIrql = (KIRQL)descriptor->u.Interrupt.Level;
                                             params.FullySpecified.InterruptMode = (descriptor->Flags & CM_RESOURCE_INTERRUPT_LATCHED) ? Latched : LevelSensitive;
                                             params.FullySpecified.ProcessorEnableMask = descriptor->u.Interrupt.Affinity;
                                             params.FullySpecified.ShareVector = descriptor->ShareDisposition;

                                             //
                                             // Default state is low.
                                             //
                                             DeviceContext->InterruptContext.State = 0;
                                             DeviceContext->InterruptContext.DeviceContext = DeviceContext;

                                             return IoConnectInterruptEx(&params);
                              }
               }

               return STATUS_SUCCESS;
}

NTSTATUS
EvtDeviceReleaseHardware(
               __in  WDFDEVICE Device,
               __in  WDFCMRESLIST ResourcesTranslated
)
{
               PDEVICE_CONTEXT DeviceContext = YourGetDeviceContext(Device);

               if (NULL != DeviceContext->Interrupt)
               {
                              IO_DISCONNECT_INTERRUPT_PARAMETERS params;

                              params.Version = CONNECT_FULLY_SPECIFIED;
                              params.ConnectionContext.InterruptObject = DeviceContext->Interrupt;

                              IoDisconnectInterruptEx(&params);
               }

               return STATUS_SUCCESS;
}
```

上記のコード例では、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数によって、デバイスコンテキストが構成され、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンを登録するために[**Ioinitializer edpcreクエスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializedpcrequest)が呼び出されます。

ドライバーの[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンは、割り込み状態の値を反転し、 [**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出して DPC をキューに置いています。

[*EvtdeviceIoConnectInterruptEx ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数では、ドライバーは状態値を**FALSE**に初期化し、次に[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を呼び出します。 [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数では、ドライバーは[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)を呼び出して、ISR の登録を解除します。

 

 





