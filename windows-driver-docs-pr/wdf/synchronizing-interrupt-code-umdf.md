---
title: 割り込みコードの同期
description: 割り込みコードの同期
ms.assetid: 5E2D0063-2251-40B3-8982-46001E67EB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b7da0609d5fbc9c09ee229ecf410ba799a58c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581729"
---
# <a name="synchronizing-interrupt-code"></a>割り込みコードの同期


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ルーチンを 1 つだけでデータにアクセスできるように、割り込みのデータ バッファーにアクセスするすべてのドライバー コードを同期する必要があります。

手動の割り込みのロックまたは自動のコールバックのシリアル化のいずれかを使用して、割り込みのコードを同期できます。

## <a name="manual-interrupt-locking"></a>手動の割り込みのロック


UMDF が呼び出す前に割り込みロックを取得、 [ *OnInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/hh463902)、 [ *OnInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/hh463895)、または[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)コールバック。

ドライバーを同期する必要がある場合は、割り込みのロックを使用してコードを呼び出します[ **IWDFInterrupt::AcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451289)と[ **IWDFInterrupt::ReleaseInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451319). たとえば、ドライバーを取得し、割り込みのロックを解放その[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)これらのメソッドを使用してコールバック ルーチン。 ただし、I/O のコールバックをディスパッチ (など[ **OnRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556875)と[ **OnWrite**](https://msdn.microsoft.com/library/windows/hardware/ff556885))、ドライバーの最初の呼び出し[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451332)をキューに作業項目または潜在的なデッドロックを回避するために同じスレッドで作業するかどうかを決定します。 呼び出すことによって生じるおそれのあるデッドロックのシナリオの例については**IWDFInterrupt::AcquireInterruptLock**任意のスレッド コンテキストからの「解説」を参照してください。 [ **IWDFInterrupt:。AcquireInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451289)します。

場合[ **IWDFInterrupt::TryToAcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh451332)返します**TRUE**ドライバーが同じスレッドで割り込みロックを獲得します。 この場合、ドライバーを呼び出して、そのロックを必要な作業を実行します。 [ **ReleaseInterruptLock**](https://msdn.microsoft.com/library/windows/hardware/hh451319)します。 場合**IWDFInterrupt::TryToAcquireInterruptLock**返します**FALSE**、ドライバー、作業項目をキューに配置しで作業を実行しますその[ *OnWorkItem* 。](https://msdn.microsoft.com/library/windows/hardware/hh463909)コールバック。 この場合は、作業項目は自動シリアル化を使用する必要があります。

## <a name="using-automatic-serialization"></a>自動シリアル化の使用


UMDF ドライバーは、呼び出すことによってコールバックの自動同期を要求できます[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)で、 *LockType*パラメーターに設定**WdfDeviceLevel**します。

ドライバーを設定し、 **AutomaticSerialization**のメンバー、 [ **WUDF\_割り込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/hh464084)構造体を**は TRUE。** 呼び出す前に[ **CreateInterrupt**](https://msdn.microsoft.com/library/windows/hardware/hh451208)します。

その結果、UMDF がドライバーのシリアル化します[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905) I/O キューを使用したコールバック要求の取り消し、およびオブジェクトのコールバック ルーチンをファイルします。 このシナリオでは、UMDF は割り込みオブジェクトのロックではなく、コールバックのロックを使用します。

 

 





