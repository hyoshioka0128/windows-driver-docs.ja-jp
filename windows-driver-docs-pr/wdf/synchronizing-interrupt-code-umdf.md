---
title: 割り込みコードの同期
description: 割り込みコードの同期
ms.assetid: 5E2D0063-2251-40B3-8982-46001E67EB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7b583ea939379978923687acbf9d674ea98b18a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375036"
---
# <a name="synchronizing-interrupt-code"></a>割り込みコードの同期


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ルーチンを 1 つだけでデータにアクセスできるように、割り込みのデータ バッファーにアクセスするすべてのドライバー コードを同期する必要があります。

手動の割り込みのロックまたは自動のコールバックのシリアル化のいずれかを使用して、割り込みのコードを同期できます。

## <a name="manual-interrupt-locking"></a>手動の割り込みのロック


UMDF が呼び出す前に割り込みロックを取得、 [ *OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)、 [ *OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)、または[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)コールバック。

ドライバーを同期する必要がある場合は、割り込みのロックを使用してコードを呼び出します[ **IWDFInterrupt::AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock)と[ **IWDFInterrupt::ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock). たとえば、ドライバーを取得し、割り込みのロックを解放その[ *OnInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)これらのメソッドを使用してコールバック ルーチン。 ただし、I/O のコールバックをディスパッチ (など[ **OnRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread)と[ **OnWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite))、ドライバーの最初の呼び出し[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock)をキューに作業項目または潜在的なデッドロックを回避するために同じスレッドで作業するかどうかを決定します。 呼び出すことによって生じるおそれのあるデッドロックのシナリオの例については**IWDFInterrupt::AcquireInterruptLock**任意のスレッド コンテキストからの「解説」を参照してください。 [ **IWDFInterrupt:。AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock)します。

場合[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock)返します**TRUE**ドライバーが同じスレッドで割り込みロックを獲得します。 この場合、ドライバーを呼び出して、そのロックを必要な作業を実行します。 [ **ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock)します。 場合**IWDFInterrupt::TryToAcquireInterruptLock**返します**FALSE**、ドライバー、作業項目をキューに配置しで作業を実行しますその[ *OnWorkItem* 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック。 この場合は、作業項目は自動シリアル化を使用する必要があります。

## <a name="using-automatic-serialization"></a>自動シリアル化の使用


UMDF ドライバーは、呼び出すことによってコールバックの自動同期を要求できます[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)で、 *LockType*パラメーターに設定**WdfDeviceLevel**します。

ドライバーを設定し、 **AutomaticSerialization**のメンバー、 [ **WUDF\_割り込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config)構造体を**は TRUE。** 呼び出す前に[ **CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)します。

その結果、UMDF がドライバーのシリアル化します[ *OnInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem) I/O キューを使用したコールバック要求の取り消し、およびオブジェクトのコールバック ルーチンをファイルします。 このシナリオでは、UMDF は割り込みオブジェクトのロックではなく、コールバックのロックを使用します。

 

 





