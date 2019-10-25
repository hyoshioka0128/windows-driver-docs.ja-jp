---
title: GpioClx DDI のドライバー サポート メソッド
description: GPIO framework 拡張機能 (GpioClx) は、Windows 8 以降で使用できます。
ms.assetid: 179EFB06-6122-4EB0-B9F8-D5A3089D75EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9162210aa3a1eb0ad0141346057d6f35f6eceebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825052"
---
# <a name="driver-support-methods-in-the-gpioclx-ddi"></a>GpioClx DDI のドライバー サポート メソッド


GPIO framework 拡張機能 (GpioClx) は、Windows 8 以降で使用できます。 GpioClx DDI のシステム提供のメソッドは、GpioClx カーネルモードドライバーである Msgpioclx に実装されています。 このドライバーは、 [Gpioclx ドライバーのサポートメソッド](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))のエントリポイントをエクスポートします。 Windows 8 以降では、Msgpioclx はオペレーティングシステムの標準コンポーネントです。

ビルド時に、GPIO コントローラードライバーは GpioClx スタブライブラリの DDI エントリポイントに静的にリンクします。 Msgpioclxstub。 実行時に、このライブラリは必要なドライバーバージョンのネゴシエーションを実行して、Msgpioclx 内の対応するエントリポイントに動的にリンクします。

特定のバージョンの Msgpioclx を必要とする GPIO コントローラードライバーは、より高いバージョン番号を持つ Msgpioclx のバージョンに安全にリンクできます。 ただし、このドライバーは、バージョン番号が小さい Msgpioclx のバージョンにリンクすることはできません。

## <a name="driver-registration"></a>ドライバーの登録


GpioClx のクライアントとして登録するために、GPIO コントローラードライバーは、 [**gpio\_CLX\_RegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)メソッドを呼び出します。 通常、ドライバーは[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンからこのメソッドを呼び出します。 この呼び出し中に、ドライバーは登録パケットをメソッドに渡します。 このパケットには、ドライバーによって実装された一連のイベントコールバック関数へのポインターが含まれています。 これらの関数は、GPIO コントローラーデバイス内のハードウェアレジスタにアクセスします。 GpioClx は、i/o 要求を処理し、割り込みを管理するために、これらの関数を呼び出します。

GPIO コントローラードライバーは、 [**gpio\_clx\_UnregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_unregisterclient)メソッドを呼び出して、GpioClx への登録をキャンセルします。 通常、ドライバーは、 [*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)イベントコールバック関数からこのメソッドを呼び出します。

## <a name="device-object-initialization"></a>デバイスオブジェクトの初期化


GpioClx を初期化するには、GPIO コントローラードライバーが[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から2つの gpioclx メソッドを呼び出す必要があります。 最初のメソッドである[**GPIO\_CLX\_ProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepredevicecreate)は、デバイスオブジェクトを作成する[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)メソッドの呼び出しの前に呼び出す必要があります。 2番目のメソッドである[**GPIO\_CLX\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)は、 **WdfDeviceCreate**呼び出しの後に呼び出す必要があります。

## <a name="interrupt-lock"></a>割り込みロック


ドライバーで実装されたイベントコールバック関数の大部分は、IRQL = パッシブ\_レベルの GpioClx でのみ呼び出されます。 ただし、次の一覧のコールバック関数は、[*クライアント\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) callback 関数が GpioClx に提供するデバイス情報に応じて、パッシブ\_レベルまたは dirql で呼び出されます。

-   [*クライアント\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
-   [*クライアント\_マスク割り込み*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
-   [*クライアント\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
-   [*クライアント\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)
-   [*クライアント\_アンマスク割り込み*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)

これらの関数は GpioClx の割り込みサービスルーチン (ISR) から呼び出されます。これは、GPIO コントローラーのハードウェアレジスタがメモリマップトかどうかに応じて、DIRQL またはパッシブ\_レベルで実行されます。

*クライアント\_Querycontroller Basicinformation*関数は、[**クライアント\_コントローラー\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)構造の形式でデバイス情報を提供します。 **MemoryMappedController**フラグビットがこの構造体の**Flags**メンバーで設定されている場合、GpioClx ISR は、前の一覧にある dirql のコールバック関数を呼び出します。 それ以外の場合、ISR は、ドライバーによって実装されたすべてのコールバック関数をパッシブ\_レベルで呼び出します。 このフラグビットの詳細については、「[割り込み関連のコールバック](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)」を参照してください。

GpioClx は、パッシブ\_レベルで実行され、GpioClx ISR から呼び出されない、ドライバーによって実装されたコールバック関数の呼び出しを自動的に同期します。 そのため、これらの関数のうち1つだけを同時に実行できます。 ただし、GpioClx では、これらのパッシブ\_レベルのコールバックは、その ISR から GpioClx が行うコールバックと自動的に同期されません。 必要に応じて、このような同期を明示的に指定する必要があります。

潜在的な同期エラーを回避するために、GpioClx は、GPIO コントローラードライバーが取得および解放できる*割り込みロック*を実装します。 割り込みロックは、主にドライバーの[*クライアント\_enableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)および[*クライアント\_disableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) callback 関数によって使用されます。 ドライバーは、 [**gpio\_clx\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)メソッドを呼び出してロックを取得し、 [**gpio\_Clx\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)メソッドを呼び出してロックを解除します。 ドライバーは、パッシブ\_レベルで呼び出されるコールバック関数からこれらのメソッドを呼び出し、GpioClx の ISR からは呼び出されません。 ドライバーがロックを保持している間、GpioClx ISR を実行できません。 ドライバーは、ISR と同期する必要がある重要な操作中にのみ、ロックを一時的に保持する必要があります。

GpioClx ISR がドライバーによって実装されたコールバック関数を呼び出す場合、この関数は、ISR が既にロックを保持している (および解放する) ため、割り込みロックを取得 (または解放) する必要はありません。 この関数による[**gpio\_clx\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)および[**GPIO\_clx x**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)の呼び出しメソッドの呼び出しは無効ですが、エラーとして扱われません。

 

 




