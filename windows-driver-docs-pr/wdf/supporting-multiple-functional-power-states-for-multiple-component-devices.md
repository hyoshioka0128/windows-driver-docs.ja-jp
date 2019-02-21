---
title: 複数コンポーネントのデバイス、1 つまたは複数の機能の電力状態
description: 1 つまたは複数の機能の電力状態での複数コンポーネントのデバイスのサポート
ms.assetid: D601A0F6-A035-4161-879A-D495518E7EC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d91b5bc63d0c7913db3bdd0c0fb106339fce3c3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549242"
---
# <a name="supporting-multiple-component-devices-with-single-or-multiple-functional-power-states"></a>1 つまたは複数の機能の電力状態での複数コンポーネントのデバイスのサポート


\[KMDF にのみ適用されます。\]

複数コンポーネントのデバイスの KMDF ドライバーでは、各コンポーネントの 1 つまたは複数の機能の電源状態を定義できます。

この場合、ドライバーは、電源管理フレームワーク (PoFx) と直接登録します。 呼び出し、WDF 登録しないでください、PoFx でドライバーを指定するのには[ **WdfDeviceAssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545903)で、 **IdleTimeoutType**のメンバー、 [**WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551270)構造体を設定**DriverManagedIdleTimeout**. 通常、ドライバーはからには、このメソッドを呼び出してその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。

次に、ドライバーは、PoFx を登録する必要があります。 そのためをドライバーの呼び出しに[ **PoFxRegisterDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh439521)し[ **PoFxStartDevicePowerManagement**](https://msdn.microsoft.com/library/windows/hardware/hh439551)します。 デバイスが初めて起動したときに、ドライバーが PoFx を 1 回だけ登録する必要があります。 ドライバーによって提供されるからこれらのルーチンを呼び出すことではこれを行う方法の 1 つ[ *EvtDeviceSelfManagedIoInit* ](https://msdn.microsoft.com/library/windows/hardware/ff540902)関数。 *EvtDeviceSelfManagedIoInit*最初にデバイスを起動するときにのみと呼びます。

デバイスを削除すると、ドライバーで呼び出す必要があります[ **PoFxUnregisterDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh439558) PoFx からデバイスの登録を解除します。 1 回をお勧めドライバー呼び出しからドライバーによって提供されるこのルーチンのみの登録を解除する[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)関数。 *EvtDeviceSelfManagedIoFlush*デバイスが削除されるときにのみ呼び出されます。 登録を解除して*EvtDeviceSelfManagedIoFlush*ドライバーは、スリープ中に電源登録を保持、および再調整は、遷移し、保留状態のまま I/O 要求の電源の参照を維持する必要はありませんこれらの中に遷移します。

ドライバーを呼び出すと[ *PoFxRegisterDevice*](https://msdn.microsoft.com/library/windows/hardware/hh406408)を受け取るように、次のトピックで説明されている、PoFx と直接対話に使用できる電源登録ハンドル (POHANDLE)。

-   [コンポーネントの電源状態の I/O 要求の調整](coordinating-i-o-requests-with-component-power-state.md)
-   [デバイスの電源オン S0 にシステムが返されるときにレポートの作成](reporting-device-powered-on.md)
-   [複数コンポーネントのデバイスでのアイドル状態の電源のサポート](supporting-idle-power-down-on-multiple-component-devices.md)

さらに、ドライバーを呼び出すことができます[framework ルーチンの電源を](https://msdn.microsoft.com/library/windows/hardware/hh450961)power control の要求を送信して、待機時間の指定に直接保存場所、およびウェイク要件。

PoFx の詳細については、次を参照してください。 [、電源管理フレームワークの概要](https://msdn.microsoft.com/library/windows/hardware/hh406637)します。

 

 





