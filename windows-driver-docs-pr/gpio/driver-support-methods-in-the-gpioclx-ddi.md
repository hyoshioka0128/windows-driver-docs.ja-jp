---
title: GpioClx DDI のドライバー サポート メソッド
description: GPIO フレームワーク拡張機能 (GpioClx) では、Windows 8 以降で使用できます。
ms.assetid: 179EFB06-6122-4EB0-B9F8-D5A3089D75EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cf41f9041ec4305431baeb2819344a8b98ad2aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363640"
---
# <a name="driver-support-methods-in-the-gpioclx-ddi"></a>GpioClx DDI のドライバー サポート メソッド


GPIO フレームワーク拡張機能 (GpioClx) では、Windows 8 以降で使用できます。 システム提供の GpioClx DDI メソッドは、Msgpioclx.sys GpioClx カーネル モード ドライバーに実装されます。 このドライバーのエントリ ポイントのエクスポート、 [GpioClx ドライバー サポート メソッド](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))します。 Windows 8 以降、Msgpioclx.sys は、オペレーティング システムの標準的なコンポーネントです。

ビルド時に、GPIO コント ローラーのドライバーは GpioClx スタブ ライブラリ、Msgpioclxstub.lib DDI エントリ ポイントに静的にリンクします。 実行時に、このライブラリは、Msgpioclx.sys で対応するエントリ ポイントに動的にリンクするために必要なドライバーのバージョンのネゴシエーションを実行します。

Msgpioclx.sys の特定のバージョンを必要とする GPIO コント ローラーのドライバーより高いバージョン番号を持つ Msgpioclx.sys のバージョンに安全にリンクできます。 ただし、このドライバーは、バージョン番号が低い Msgpioclx.sys のバージョンにリンクできません。

## <a name="driver-registration"></a>ドライバーの登録


GPIO コント ローラーのドライバーを呼び出す GpioClx のクライアントとして登録するには[ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)メソッド。 通常、ドライバーはからには、このメソッドを呼び出してその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 この呼び出し中には、ドライバーは、登録パケットをメソッドに渡します。 このパケットには、一連のイベントのドライバーに実装されているコールバック関数へのポインターが含まれています。 これらの関数は、GPIO コント ローラー デバイスのハードウェア レジスタにアクセスします。 GpioClx は I/O 要求を処理して、割り込みを管理するこれらの関数を呼び出します。

GPIO コント ローラーのドライバーは呼び出し、 [ **GPIO\_CLX\_UnregisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_unregisterclient) GpioClx とその登録をキャンセルするメソッド。 通常、ドライバーはからには、このメソッドを呼び出してその[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)イベント コールバック関数。

## <a name="device-object-initialization"></a>デバイス オブジェクトの初期化


GpioClx を初期化するためには、GPIO コント ローラーのドライバーがから 2 つの GpioClx メソッドを呼び出す必要があります、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 最初のメソッドで[ **GPIO\_CLX\_ProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepredevicecreate)、呼び出しの前に呼び出す必要があります、 [ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)メソッドで、デバイス オブジェクトを作成します。 2 番目のメソッドでは、 [ **GPIO\_CLX\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)、後に呼び出す必要があります、 **WdfDeviceCreate**呼び出します。

## <a name="interrupt-lock"></a>ロックを中断します。


ドライバーに実装されているイベントのコールバック関数の大半は IRQL でのみと呼ばれる = パッシブ\_GpioClx によってレベル。 ただし、次の一覧のコールバック関数を呼び出すはのいずれかパッシブで\_レベルまたはデバイスの情報に応じて、DIRQL を[*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) GpioClx にコールバック関数を提供します。

-   [*クライアント\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
-   [*クライアント\_MaskInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
-   [*クライアント\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
-   [*クライアント\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)
-   [*クライアント\_UnmaskInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)

これらの関数は、GpioClx DIRQL またはパッシブのいずれかの実行に割り込みサービス ルーチン (ISR) から呼び出される\_GPIO コント ローラーのハードウェア レジスタは、メモリ マップできるかどうかに応じて、レベル。

*クライアント\_QueryControllerBasicInformation*関数の形式でデバイス情報を提供する[**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)構造体。 場合、 **MemoryMappedController**でフラグ ビットが設定されて、**フラグ**DIRQL で上記のリストをこの構造体のメンバーは、GpioClx ISR 呼び出すコールバック関数。 それ以外の場合、パッシブでが ISR 呼び出すすべてのドライバーによって実装されるコールバック関数\_レベル。 このフラグのビットの詳細については、次を参照してください。 [Interrupt-Related コールバック](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)します。

GpioClx はパッシブで実行されるドライバーによって実装されるコールバック関数への呼び出しを自動的に同期\_GpioClx ISR から呼び出されていないレベルとは したがって、これらの関数の 1 つだけを一度に実行できます。 ただし、GpioClx でこれらパッシブが自動的に同期されていない\_GpioClx によりその ISR. からのコールバックを使用したレベルのコールバック GPIO コント ローラーのドライバーは、必要な場合、このような同期を明示的に指定する必要があります。

GpioClx を実装する潜在的な同期エラーを回避するために、 *interrupt ロック*GPIO コント ローラーのドライバーが取得および解放します。 割り込みロックは、主に、ドライバーの使用[*クライアント\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)と[*クライアント\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)コールバック関数。 ドライバーの呼び出し、 [ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)ロック、および呼び出しを取得するメソッド、 [ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)ロックを解放するメソッド。 ドライバーはパッシブで呼び出されるコールバック関数からこれらのメソッドを呼び出す\_レベルと GpioClx の ISR からは呼び出されません。 ドライバーは、ロックを保持している間、GpioClx ISR は実行できません。 ドライバーは短期間だけロックを保持する必要があり。 する、重要な操作中にのみ ISR と同期する必要があります。

GpioClx ISR ドライバー実装の呼び出しのコールバック関数、この関数でない場合必要があります (またはリリース) を取得する割り込みためにロック ISR 既にロックを保持して (およびそれを解放)。 呼び出し、 [ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)と[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)メソッドをこの関数では、効果はありませんが、エラーとして扱われません。

 

 




