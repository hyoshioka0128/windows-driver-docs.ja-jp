---
title: デバイスのウェイクに対する割り込みの使用
description: デバイスは、低電力状態に遷移、ときに、フレームワークが切断されます (または非アクティブとして報告) I/O に使用される割り込みを処理します。
ms.assetid: 6A4E62BD-B10F-4F01-B4B4-1FF5086710D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c618dea1cdc8b54bd11579df398b9b19aa1a6895
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363476"
---
# <a name="using-an-interrupt-to-wake-a-device"></a>デバイスのウェイクに対する割り込みの使用


デバイスは、低電力状態に遷移、ときに、フレームワークが切断されます (または非アクティブとして報告) I/O に使用される割り込みを処理します。 KMDF 以降 1.13 および UMDF 2.0 は Windows 8.1 で実行されている、WDF ドライバー オブジェクトを作成できます framework 割り込みをアクティブなままデバイスが、低電力状態に遷移し、デバイスがスリープ解除して、完全に D0 状態に復元するために使用するとします。

チップ (SoC) プラットフォーム上のシステムを WDF ドライバーを開発している場合は、従来のウェイク信号メカニズムを提供していないデバイスがスリープ解除するこのような割り込みを使用できます。 この機能を使用するには、デバイスを ACPI を介して公開され、ウェイク アップの割り込みのハードウェアのサポートが必要です。 割り込みを作成するドライバーは、デバイスの電源ポリシーの所有者である必要があります。

デバイスは、低電力状態に遷移、ときに、フレームワークはウェイク対応として識別されている、割り込みを切断しません。 デバイスが割り込み、ときにフレームワークのドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)と[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)でコールバック ルーチンIRQL = パッシブ\_レベル。

ドライバーが既に作成した場合、[パッシブ レベル割り込みオブジェクト](supporting-passive-level-interrupts.md)I/O 処理のためお勧めしますウェイク アップ機能を同じ割り込みオブジェクトを共有します。 このシナリオで、ドライバーの[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック ルーチンを O 関連の割り込みの処理を実行できるだけでなく、処理をスリープ解除の条件付きロジックを実装します。

ただし、デバイスの IRQL (DIRQL) での処理を必要と割り込みを使う場合は、ウェイク アップ機能を提供する追加のフレームワーク割り込みオブジェクトを作成するを勧めします。

KMDF または UMDF ドライバー ウェイク対応割り込みオブジェクトを作成する次の手順に従います。

1.  呼び出す[ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)、通常はから[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)を指定して**IdleCanWakeFromS0**で、 *IdleCaps*パラメーター。
2.  必要に応じて、呼び出す[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)で説明されているイベントのコールバック関数を登録する[システムのウェイク アップをサポートしている](supporting-system-wake-up.md)します。
3.  呼び出す[ **WDF\_INTERRUPT\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552348)初期化するために、 [ **WDF\_INTERRUPT\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)構造体。 提供、 [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)パッシブ レベルで呼び出されるコールバック関数。 構成構造体で設定**PassiveHandling**と**CanWakeDevice**に**TRUE**します。 呼び出して[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)からドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)フレームワークを作成するコールバック関数割り込みオブジェクト。
4.  呼び出す[ **WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909)低電力状態からシステムをスリープ解除するデバイスを構成します。
    ```cpp
    WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
    wakeSettings.DxState = PowerDeviceD3;
    wakeSettings.UserControlOfWakeSettings = WakeDoNotAllowUserControl;
    wakeSettings.Enabled = WdfTrue;

    status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
    if (!NT_SUCCESS(status)) {
        Trace(TRACE_LEVEL_ERROR,"WdfDeviceAssignSxWakeSettings failed %x\n", status);
        return status;
    }
    ```

5.  デバイスは、低電力状態に遷移、ときにフレームワークを呼び出しません[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)ウェイク対応の割り込みの。 フレームワークが呼び出す[ *EvtDeviceArmWakeFromS0* ](https://msdn.microsoft.com/library/windows/hardware/ff540843)ドライバーが 1 つ指定されている場合。
6.  ドライバーのフレームワークと、デバイスが、ウェイク割り込みシグナル、 [ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック ルーチン。
7.  場合、ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバックは、成功を返します、フレームワークは、ドライバーの[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバックパッシブ レベル。 割り込みハンドラーから制御が戻る前に割り込みコント ローラーに割り込みを無音にする必要があります。 ドライバーからエラー コードが返らない場合*EvtDeviceD0Entry*、フレームワークは、割り込みを切断し、呼び出し、ドライバーの[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバックの場合、1 つのドライバーを提供しています。
8.  フレームワークは、ドライバーが提供されるいずれかの場合に、次ウェイク イベント コールバック ルーチンを呼び出します。
    -   [*EvtDeviceDisarmWakeFromS0*](https://msdn.microsoft.com/library/windows/hardware/ff540860)
    -   [*EvtDeviceDisarmWakeFromSx*](https://msdn.microsoft.com/library/windows/hardware/ff540862)
    -   [*EvtDeviceWakeFromS0Triggered*](https://msdn.microsoft.com/library/windows/hardware/ff540919)
    -   [*EvtDeviceWakeFromSxTriggered*](https://msdn.microsoft.com/library/windows/hardware/ff540923)

9.  フレームワークは」の説明に従って、通常の電源投入コールバック シーケンスで引き続き[関数またはフィルター ドライバーの電源投入シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)します。

使用することができます、 [ **! wdfkd.wdfinterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff565787)デバッガー拡張機能をウェイク アップに対応する特定の割り込みが構成されているかどうかを表示します。

ウェイク アップの中断機能は、USB のセレクティブと組み合わせて使用することはできませんを中断します。

 

 





