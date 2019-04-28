---
title: Active-Both 割り込みの処理
description: Active-Both 割り込みの処理
ms.assetid: CFA205B1-FDDD-4E27-8CF9-106C8D1CC4EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a72528f4cadb34bd9c91b75385dca8370bc0b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366494"
---
# <a name="handling-active-both-interrupts"></a>Active-Both 割り込みの処理


**注**  このトピックには、のみをカーネル モード ドライバー フレームワーク (KMDF) 1.13 およびそれ以前のバージョンが適用されます。

 

多くのデバイスでは、その割り込みの生成を制御し、マスク ハードウェア レジスタがあります。 通常、このようなデバイス ドライバー KMDF および UMDF ドライバーは、組み込みの割り込みのフレームワークのサポートを使用します。

ただし、チップ (SoC) のハードウェア プラットフォーム上のシステム上の単純なデバイスでは、割り込みのハードウェア レジスタがあります。 結果としてのようなデバイス ドライバーが割り込みが生成されるときにコントロールをことができるいない、またはハードウェアの割り込みをマスクすることができる可能性があります。 デバイスが接続時にすぐに中断して、ドライバーは割り込みのフレームワークのサポートを使用して、フレームワーク、framework 割り込みオブジェクトの初期化が完了する前に割り込み可能性が。 その結果、KMDF ドライバーでは、接続し、切断の割り込みを直接 WDM ルーチンを呼び出す必要があります。 UMDF ドライバーでは、これらのメソッドを呼び出すことはできません、ために、このようなデバイスの UMDF ドライバーを記述することはできません。

このトピックでは、KMDF ドライバーがこのようなデバイスの割り込みを処理する方法について説明します。

SoC のハードウェア プラットフォームでアクティブ両方の割り込みは通常、ハードウェアのプッシュ ボタンのような非常に単純なデバイスを使用します。 ユーザーは、クリック 1 回押すと、デバイスからの割り込みシグナル線低から高、または高からに移行低します。 ユーザーはリリース、プッシュ ボタン、割り込みの線は反対方向に遷移します。 GPIO ピン構成アクティブ両方の割り込みの入力が、システムのどちらの場合も、周辺機器のデバイス ドライバーの割り込みサービス ルーチン (ISR) を呼び出すことで、低-高と高から低の両方の遷移の割り込みを生成します。 ただし、ドライバーの移行が低-高または高から低かどうかを示す値を受け取りませんしません。

低-高と高から低の遷移を区別するために、ドライバーは、各割り込みの状態を追跡する必要があります。 これを行うには、ドライバーがブール割り込み状態の値であるを維持可能性があります**FALSE**割り込み回線の状態が低いときと**TRUE**行の状態が高い場合。

たとえば、システムの起動時に低に回線の状態が既定値があるとします。 ドライバーの初期化に状態値**FALSE**でその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。 状態の変化のシグナル、ドライバーの ISR が呼び出されるたびに、ドライバーを反転その ISR. で状態の値

回線の状態が高い場合、システムの起動時に有効にした後すぐに割り込みが発生します。 ドライバーを呼び出すため、 [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)呼び出す代わりに直接、日常的な[ **WdfInterruptCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547345)は即時割り込みの受信のことを確認します。

このソリューションでは、GPIO コント ローラーが、ハードウェアの割り込みのアクティブ両方をサポートすることや、GPIO コント ローラー用ドライバーがのソフトウェアのアクティブな両方の割り込みをエミュレートすることが必要です。 アクティブな両方の割り込みをエミュレートする方法の詳細については、の説明を参照して、 **EmulateActiveBoth**のメンバー、 [**コント ローラー\_属性\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh439449)構造体。

次のコード例では、周辺機器の KMDF ドライバーが割り込み極性を追跡する方法を示します。

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

上記のコードの例で、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数は、デバイス コンテキストを構成しを呼び出して[ **IoInitializeDpcRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549307)を登録する、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン。

ドライバーの[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチンが割り込み状態の値を反転し、呼び出します[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657) DPC キューに登録します。

その[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数では、ドライバーを初期化する状態値**FALSE**号餧ェヒェマル[ **IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)します。 その[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数では、ドライバー呼び出し[ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093)その ISR. の登録を解除するには

 

 





