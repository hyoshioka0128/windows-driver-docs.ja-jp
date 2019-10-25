---
title: GPIO コントローラー ドライバーの割り込み同期
description: GPIO controller ドライバーは、GPIO_CLX_AcquireInterruptLock メソッドと GPIO_CLX_ReleaseInterruptLock メソッドを呼び出して、GPIO フレームワーク拡張機能 (GpioClx) によって内部的に実装されている割り込みロックを取得し、解放します。
ms.assetid: D9698A50-7CC2-463C-9E46-7FE428F3193E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b456369b600ae0ba23ebfe38616f52f6f9f6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824938"
---
# <a name="interrupt-synchronization-for-gpio-controller-drivers"></a>GPIO コントローラー ドライバーの割り込み同期


Gpio コントローラードライバーは、gpio [ **\_clx\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)および[**gpio\_Clx\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)メソッドを呼び出して、gpio によって内部的に実装されている割り込みロックを取得し、解放します。フレームワーク拡張 (GpioClx)。 IRQL = パッシブ\_レベルで実行されるドライバーコードは、これらのメソッドを呼び出して、GpioClx の割り込みサービスルーチン (ISR) と同期できます。 GpioClx は、GPIO コントローラー内の各ピンのバンクに個別の割り込みロックを専用にします。

GPIO コントローラーのハードウェアレジスタがメモリにマップされている場合、GpioClx の ISR は、特定のドライバーによって実装されたイベントコールバック関数を DIRQL に呼び出します。GpioClx は、パッシブ\_レベルでコールバック関数の残りの部分を呼び出します。 レジスタのバンクにアクセスするパッシブレベルのコールバック関数では、割り込みロックを使用して、DIRQL で実行され、同じレジスタにアクセスするコールバック関数に同期する必要がある場合があります。

たとえば、パッシブレベルの[*クライアント\_enableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)と[*クライアント\_disableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) CALLBACK 関数は、dirql で実行される他の割り込み関連コールバックルーチンの操作に影響するハードウェア設定を変更します。 *クライアント\_enableinterrupt*関数と*クライアント\_disableinterrupt*関数は、通常、銀行の割り込みロックを使用して、登録アクセスを同期します。

GpioClx は、DIRQL で発生する割り込み関連および i/o 関連のコールバックを自動的にシリアル化します。 GpioClx は、DIRQL でコールバック関数を呼び出す前にターゲットバンクの割り込みロックを取得し、関数から制御が戻った後にロックを解放します。 DIRQL で呼び出されるコールバック関数が、 **GPIO\_CLX\_AcquireInterruptLock**を呼び出すことによって、バンクの割り込みロックを再取得しようとするとエラーになります。

同様に、GpioClx は、パッシブ\_レベルで発生するコールバックを自動的にシリアル化します。 GpioClx は、銀行ごとに待機ロックを内部的に実装します。 GpioClx は、パッシブ\_レベルでコールバック関数を呼び出す前にターゲットバンクの待機ロックを取得し、関数から制御が戻ったときにロックを解放します。 メモリマップされた GPIO コントローラーの場合、GpioClx はドライバーに代わって銀行の待機ロックを管理しますが、ドライバーが明示的にロックを取得して解放することはできません。

ただし、メモリにマップされていない GPIO コントローラーの場合、 **gpio\_clx\_AcquireInterruptLock**および**GPIO\_Clx\_ReleaseInterruptLock**は、割り込みロックではなく待機ロックを取得して解放します。 GpioClx は、GPIO コントローラーのピンのバンクごとに個別の待機ロックを実装します。 レジスタはメモリにマップされていないため、割り込み関連および i/o 関連のコールバック関数はすべて、パッシブ\_レベルで呼び出されます。これにより、i/o 要求を使用して、I ² C などのシリアルバスを介してレジスタにアクセスできるようになります。 GpioClx は、これらのコールバック関数のいずれかを呼び出す前にターゲットバンクの待機ロックを取得し、関数から制御が戻った後にロックを解放します。

メモリにマップされていないコントローラーのコールバック関数が、 **GPIO\_CLX\_AcquireInterruptLock**を呼び出すことによって、バンク待機ロックを再取得しようとするとエラーになります。 ただし、コールバック関数の外部にあるパッシブレベルのドライバーコードでは、 **GPIO\_CLX\_*Xxx*InterruptLock**メソッドを呼び出して、コールバック関数と同期することができます。 GpioClx は、すべての割り込み関連および i/o 関連のコールバック関数をパッシブ\_レベルで呼び出します。そのため、銀行の待機ロックは、メモリにマップされていないコントローラーの銀行の割り込みロックの代わりに効果的に使用されます。

メモリにマップされていないコントローラーのもう1つのオプションは、コントローラードライバーが待機ロックのセットを実装することです。 これらの待機ロックによって、コールバックルーチンは、GpioClx によって実装された待機ロックで可能な限り、共有リソースの粒度の細かいロックとロック解除を行うことができます。

[*クライアント\_querycontroller Basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) callback ルーチンの呼び出し中に、コントローラーレジスタがメモリマップトであるかどうかを、GPIO コントローラードライバーが GpioClx に報告します。 詳細については、「 [**CLIENT\_CONTROLLER\_基本的な\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)」の**MemoryMappedController**フラグの説明を参照してください。

割り込みロックと待機ロックの詳細については、「 [Using Framework locks](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-locks)」を参照してください。

次の表は、レジスタがメモリマップトである場合に、パッシブ\_レベルではなく DIRQL で呼び出されるコールバック関数について詳しく説明しています。 表に従って、パッシブレベルのコールバック関数で割り込みロックを使用する場合の注意事項を説明します。

-   [割り込み関連のコールバック関数](#interrupt-related-callback-functions)
-   [I/o 関連のコールバック関数](#io-related-callback-functions)
-   [GPIO 初期化とセットアップ関連のコールバック関数](#gpio-initialization-and-setup-related-callback-functions)
-   [GPIO 電源管理関連のコールバック関数](#gpio-power-management-related-callback-functions)
-   [その他のコールバック関数](#other-callback-functions)

## <a name="interrupt-related-callback-functions"></a>割り込み関連のコールバック関数


割り込み入力として構成されている GPIO pin をサポートするために、GPIO コントローラードライバーは、これらの pin を使用して割り込み要求を管理するための一連のイベントコールバック関数を実装します。 次の表では、中央の列が、GPIO コントローラーのハードウェアレジスタがメモリマップトである場合に、関数が呼び出される IRQL を示しています。 右端の列は、レジスタがメモリマップトではなく、シリアルバス経由でアクセスする必要がある場合に、関数が呼び出される IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>メモリマップトの場合は IRQL (MemoryMappedController = 1)</th>
<th>順次アクセスされる場合の IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_EnableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)"><em>CLIENT_EnableInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_DisableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)"><em>CLIENT_DisableInterrupt</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注1を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注2を参照)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_ClearActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)"><em>CLIENT_ClearActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts" data-raw-source="[&lt;em&gt;CLIENT_MaskInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)"><em>CLIENT_MaskInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)"><em>CLIENT_QueryActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryEnabledInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)"><em>CLIENT_QueryEnabledInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt" data-raw-source="[&lt;em&gt;CLIENT_ReconfigureInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)"><em>CLIENT_ReconfigureInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt" data-raw-source="[&lt;em&gt;CLIENT_UnmaskInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)"><em>CLIENT_UnmaskInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>(注3を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注4を参照)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt" data-raw-source="[&lt;em&gt;CLIENT_PreProcessControllerInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)"><em>CLIENT_PreProcessControllerInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>(注5を参照)。</p></td>
<td><p>DIRQL</p>
<p>(注6を参照)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得しません。 コールバック関数は、必要に応じて、DIRQL で実行されるコールバック関数と共有されるレジスタのアクセスを同期するために、必要に応じて銀行の割り込みロックを取得できます。

2.  GpioClx は、このコールバック関数への呼び出しを、パッシブ\_レベルで呼び出される他の割り込み関連および i/o 関連のコールバック関数とシリアル化します。 このため、コールバック関数は、bank wait ロックを取得しようとすることはできません。

3.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得し、関数から制御が戻った後にロックを解放します。 このため、コールバック関数は、バンク割り込みロックの取得を試行しません。

4.  GpioClx は、このコールバック関数への呼び出しを、パッシブ\_レベルで呼び出される他の割り込み関連および i/o 関連のコールバック関数とシリアル化します。 このため、コールバック関数は、bank wait ロックを取得しようとすることはできません。

5.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得し、関数から制御が戻った後にロックを解放します。 このため、コールバック関数は、バンク割り込みロックの取得を試行しません。

6.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得しません。 GPIO controller ドライバーは、必要になる可能性のある同期を提供する役割を担います。

## <a name="io-related-callback-functions"></a>I/o 関連のコールバック関数


データ i/o ピンとして構成されている GPIO pin をサポートするために、GPIO コントローラードライバーは、これらの pin を使用して i/o 操作を管理するための一連のイベントコールバック関数を実装します。 次の表では、中央の列が、GPIO コントローラーのハードウェアレジスタがメモリマップトである場合に、関数が呼び出される IRQL を示しています。 右端の列は、レジスタがメモリマップトではなく、シリアルバス経由でアクセスする必要がある場合に、関数が呼び出される IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>メモリマップトの場合は IRQL (MemoryMappedController = 1)</th>
<th>順次アクセスされる場合の IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_ConnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)"><em>CLIENT_ConnectIoPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_DisconnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)"><em>CLIENT_DisconnectIoPins</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注1を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注2を参照)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)"><em>CLIENT_ReadGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)"><em>CLIENT_ReadGpioPinsUsingMask</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)"><em>CLIENT_WriteGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)"><em>CLIENT_WriteGpioPinsUsingMask</em></a></p></td>
<td><p>DIRQL</p>
<p>(注3を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注4を参照)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得しません。 コールバック関数は、必要に応じて、DIRQL で実行されるコールバック関数と共有されるレジスタのアクセスを同期するために、必要に応じて割り込みロックを取得できます。

2.  GpioClx は、このコールバック関数への呼び出しを、パッシブ\_レベルで呼び出される他の割り込み関連および i/o 関連のコールバック関数とシリアル化します。 このため、コールバック関数は、bank wait ロックを取得しようとすることはできません。

3.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得し、関数から制御が戻った後にロックを解放します。 このため、コールバック関数は、バンク割り込みロックの取得を試行しません。

4.  GpioClx は、このコールバック関数への呼び出しを、パッシブ\_レベルで呼び出される他の割り込み関連および i/o 関連のコールバック関数とシリアル化します。 このため、コールバック関数は、bank wait ロックを取得しようとすることはできません。

## <a name="gpio-initialization-and-setup-related-callback-functions"></a>GPIO 初期化とセットアップ関連のコールバック関数


I/o と割り込み操作を実行するように GPIO コントローラーを設定するために、GPIO コントローラードライバーは、コントローラーを初期化する一連のイベントコールバック関数を実装します。 次の表では、中央の列が、GPIO コントローラーのハードウェアレジスタがメモリマップトである場合に、関数が呼び出される IRQL を示しています。 右端の列は、レジスタがメモリマップトではなく、シリアルバス経由でアクセスする必要がある場合に、関数が呼び出される IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>メモリマップトの場合は IRQL (MemoryMappedController = 1)</th>
<th>順次アクセスされる場合の IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller" data-raw-source="[&lt;em&gt;CLIENT_PrepareController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller)"><em>CLIENT_PrepareController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller" data-raw-source="[&lt;em&gt;CLIENT_ReleaseController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller)"><em>CLIENT_ReleaseController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller" data-raw-source="[&lt;em&gt;CLIENT_StartController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)"><em>CLIENT_StartController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller" data-raw-source="[&lt;em&gt;CLIENT_StopController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)"><em>CLIENT_StopController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information" data-raw-source="[&lt;em&gt;CLIENT_QueryControllerBasicInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)"><em>CLIENT_QueryControllerBasicInformation</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information" data-raw-source="[&lt;em&gt;CLIENT_QuerySetControllerInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)"><em>CLIENT_QuerySetControllerInformation</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注1を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注2を参照)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx がこれらのコールバック関数のいずれかを呼び出すと、バンク割り込みロックは使用できません。 このため、これらのコールバック関数は、バンク割り込みロックの取得を試行しません。

2.  これらのコールバック関数が呼び出された場合、GpioClx bank wait ロックは使用できません。 このため、ドライバーは、これらのコールバック関数と同期するために、バンク待機ロックを取得しないようにする必要があります。

## <a name="gpio-power-management-related-callback-functions"></a>GPIO 電源管理関連のコールバック関数


Gpio コントローラーでデバイスの電源状態を変更できるようにするために、GPIO コントローラードライバーは、これらの変更中にハードウェア設定を保存および復元するための一連のイベントコールバック関数を実装します。 次の表では、中央の列が、GPIO コントローラーのハードウェアレジスタがメモリマップトである場合に、関数が呼び出される IRQL を示しています。 右端の列は、レジスタがメモリマップトではなく、シリアルバス経由でアクセスする必要がある場合に、関数が呼び出される IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>メモリマップトの場合は IRQL (MemoryMappedController = 1)</th>
<th>順次アクセスされる場合の IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_RestoreBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)"><em>CLIENT_RestoreBankHardwareContext</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_SaveBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)"><em>CLIENT_SaveBankHardwareContext</em></a></p></td>
<td><p>DIRQL または HIGH_LEVEL</p>
<p>(「メモ」を参照してください)。</p></td>
<td><p>サポートされません。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

-   通常の F 状態遷移の場合: DIRQL で GpioClx に保持されている銀行の割り込みロックを使用して、保存/復元コールバック関数が呼び出されます。 したがって、どちらのコールバック関数も、バンクの割り込みロックを取得しようとしません。

<!-- -->

-   重大な F 状態遷移の場合: GPIO 状態を保存および復元するためにパワーエンジンプラグイン (PEP) が呼び出されると、保存/復元コールバックが呼び出されます。 保存/復元コールバック関数は、最後のプロセッサのコンテキストでは高\_レベルで呼び出され、アイドル状態になります。これは、プラットフォームの詳細アイドル遷移シーケンスで遅延が発生します。 したがって、どちらのコールバック関数も、バンクの割り込みロックを取得しようとしません。

F 状態の詳細については、「[コンポーネントレベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)」を参照してください。 PEP の詳細については、「 [**Pofxpowercontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)」を参照してください。

## <a name="other-callback-functions"></a>その他のコールバック関数


GPIO コントローラーがコントローラー固有の操作をサポートできるようにするために、GPIO コントローラードライバーは[*クライアント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)コントローラーのイベントコールバック関数を実装します。 次の表では、中央の列が、GPIO コントローラーのハードウェアレジスタがメモリマップトである場合に、関数が呼び出される IRQL を示しています。 右端の列は、レジスタがメモリマップトではなく、シリアルバス経由でアクセスする必要がある場合に、関数が呼び出される IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>メモリマップトの場合は IRQL (MemoryMappedController = 1)</th>
<th>順次アクセスされる場合の IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function" data-raw-source="[&lt;em&gt;CLIENT_ControllerSpecificFunction&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)"><em>CLIENT_ControllerSpecificFunction</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注1を参照)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注2を参照)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx は、このコールバック関数を呼び出す前に、バンク割り込みロックを取得しません。 コールバック関数は、必要に応じて、DIRQL で実行されるコールバック関数と共有されるレジスタのアクセスを同期するために、必要に応じて銀行の割り込みロックを取得できます。

2.  GpioClx は、このコールバック関数への呼び出しを、パッシブ\_レベルで呼び出される他の割り込み関連および i/o 関連のコールバック関数とシリアル化します。 このため、コールバック関数は、bank wait ロックを取得しようとすることはできません。

 

 




