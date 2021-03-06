---
title: GPIO コントローラー ドライバーの割り込み同期
description: GPIO コント ローラーのドライバーでは、取得および GPIO フレームワーク拡張機能 (GpioClx) によって内部的に実装される割り込みロックを解放する GPIO_CLX_AcquireInterruptLock と GPIO_CLX_ReleaseInterruptLock メソッドを呼び出すことができます。
ms.assetid: D9698A50-7CC2-463C-9E46-7FE428F3193E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37124c974c93ceb2c5120ad56ea8aef5e4bcec0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363577"
---
# <a name="interrupt-synchronization-for-gpio-controller-drivers"></a>GPIO コントローラー ドライバーの割り込み同期


GPIO コント ローラー ドライバーが呼び出すことができます、 [ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)と[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)取得および解放するメソッドは、GPIO フレームワーク拡張機能 (GpioClx) によって内部的に実装されているロックを中断します。 IRQL で実行されるドライバー コード = パッシブ\_レベル GpioClx で割り込みサービス ルーチン (ISR) に同期するこれらのメソッドを呼び出すことができます。 GpioClx 専用に GPIO コント ローラーのピンの各銀行に別の割り込みロックします。

GPIO コント ローラーのハードウェア レジスタのメモリ マッピングが、GpioClx の ISR ドライバー実装の特定のイベントのコールバック関数で呼び出します DIRQL;パッシブに、コールバック関数の残りの部分を呼び出して、GpioClx\_レベル。 レジスタの銀行にアクセスするパッシブ レベルのコールバック関数は、ロックを使用して、割り込み DIRQL で実行して、同じレジスタにアクセスするコールバック関数に同期する必要があります。

たとえば、パッシブ-レベル[*クライアント\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)と[*クライアント\_DisableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)コールバック関数が DIRQL で実行するその他の割り込みに関連するコールバック ルーチンの動作に影響するハードウェアの設定を変更します。 *クライアント\_EnableInterrupt*と*クライアント\_DisableInterrupt*関数は通常、登録のアクセスを同期する銀行の割り込みのロックを使用します。

GpioClx には、DIRQL で発生した割り込み関連および O 関連のコールバックが自動的にシリアル化します。 GpioClx では、DIRQL でコールバック関数を呼び出す前にターゲット銀行の割り込みのロックを取得し、関数が返された後にロックを解放します。 呼び出すことによって、銀行の割り込みのロックを再度取得しようとする DIRQL で呼び出されるコールバック関数のエラー **GPIO\_CLX\_AcquireInterruptLock**します。

同様に、GpioClx 自動的にシリアル化コールバック パッシブに発生する\_レベル。 GpioClx は、銀行ごとの待機のロックを内部的に実装します。 GpioClx パッシブでコールバック関数を呼び出す前にターゲット銀行のロックを待機を取得する\_レベル、し、関数が返す場合、ロックを解放します。 メモリ マップト GPIO コント ローラーの場合は、GpioClx はドライバーに代わって銀行待機ロックの管理を明示的に取得およびロックを解放するドライバーを有効にしません。

ただし、GPIO、メモリ マップト-コント ローラーの**GPIO\_CLX\_AcquireInterruptLock**と**GPIO\_CLX\_ReleaseInterruptLock**取得し、割り込みロックではなく待機ロックを解放します。 GpioClx では、GPIO コント ローラーのピンの各銀行の別の待機のロックを実装します。 レジスタがないと、メモリ マップト、割り込みに関連して、パッシブに O に関連するコールバック関数が呼び出されるため、\_レベル I/O を使用するよう要求 I²C などのシリアル バスを通じて、レジスタにアクセスします。 GpioClx では、これらのコールバック関数のいずれかを呼び出す前にターゲット銀行のロックを待機を取得し、関数が返された後にロックを解放します。

コールバック関数の呼び出すことによって銀行待機のロックを再度取得しようとするメモリ マップト-コント ローラーのエラー **GPIO\_CLX\_AcquireInterruptLock**します。 ただし、コールバック関数の外部でパッシブ レベルのドライバーのコードを呼び出すことができます、 **GPIO\_CLX\_*Xxx*InterruptLock**コールバック関数に同期する方法。 GpioClx はパッシブですべての割り込み関連および O 関連のコールバック関数を呼び出すため\_レベル、銀行待機ロック効果的にロックを取得、銀行の割り込みコント ローラーの非メモリ マップします。

メモリ マップト-コント ローラー用の別のオプションは、コント ローラー ドライバーが待機ロックのセットを実装するためです。 ロックを待ってからこれらをより細かなロックおよび GpioClx によって実装される待機ロックよりも、共有リソースのロック解除を行うにコールバック ルーチンを有効にする場合があります。

呼び出し中に、 [*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック ルーチンでは、GPIO コント ローラーのドライバーに報告 GpioClx コント ローラーのレジスタのメモリ マッピングがあるかどうか。 詳細については、の説明を参照して、 **MemoryMappedController**フラグ[**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information).

詳細については、割り込みのロックとロックの待機は、次を参照してください。[を使用して Framework ロック](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-locks)します。

次の表より詳細な情報については、どのコールバックは、関数はパッシブでの代わりに DIRQL で呼び出されます\_のメモリ マッピングが、レジスタの場合はレベルします。 次の表は、ノートでは、パッシブ レベルのコールバック関数が割り込みのロックを使用する場合について説明します。

-   [割り込みに関連するコールバック関数](#interrupt-related-callback-functions)
-   [O に関連するコールバック関数](#io-related-callback-functions)
-   [GPIO 初期化とセットアップに関連するコールバック関数](#gpio-initialization-and-setup-related-callback-functions)
-   [GPIO 電源管理に関連するコールバック関数](#gpio-power-management-related-callback-functions)
-   [その他のコールバック関数](#other-callback-functions)

## <a name="interrupt-related-callback-functions"></a>割り込みに関連するコールバック関数


割り込みの入力として構成されている GPIO ピンをサポートするためには、GPIO コント ローラーのドライバーは、一連のイベントのコールバック関数を介してこれらのピンの割り込み要求を管理するを実装します。 次の表では、中央の列は、GPIO コント ローラーのハードウェア レジスタ、メモリ マップされている場合に、関数が呼び出される IRQL を示します。 右端の列には、IRQL の場合は、レジスタのメモリ マッピングがないと、シリアル バスからアクセスする必要がありますが、関数が呼び出されることを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>IRQL if memory-mapped (MemoryMappedController = 1)</th>
<th>逐次的にアクセスする場合は、IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_EnableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)"><em>CLIENT_EnableInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_DisableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)"><em>CLIENT_DisableInterrupt</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 1 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 2 を参照してください)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_ClearActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)"><em>CLIENT_ClearActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts" data-raw-source="[&lt;em&gt;CLIENT_MaskInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)"><em>CLIENT_MaskInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)"><em>CLIENT_QueryActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryEnabledInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)"><em>CLIENT_QueryEnabledInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt" data-raw-source="[&lt;em&gt;CLIENT_ReconfigureInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)"><em>CLIENT_ReconfigureInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt" data-raw-source="[&lt;em&gt;CLIENT_UnmaskInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)"><em>CLIENT_UnmaskInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>(注 3 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 4 を参照してください)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt" data-raw-source="[&lt;em&gt;CLIENT_PreProcessControllerInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)"><em>CLIENT_PreProcessControllerInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>(注 5 を参照してください)。</p></td>
<td><p>DIRQL</p>
<p>(注 6 を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックは取得しません。 DIRQL で実行される関数の必要に応じて、コールバックで共有されているレジスタのアクセスを同期する場合、コールバック関数は、銀行の割り込みロックを取得できます。

2.  GpioClx パッシブで呼び出されるその他の割り込み関連および O 関連のコールバック関数では、このコールバック関数への呼び出しをシリアル化\_レベル。 そのため、コールバック関数は、銀行の待機をロックする必要があります試みません。

3.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックを取得し、関数が返された後にロックを解放します。 そのため、コールバック関数は、銀行の割り込みのロックを取得する必要があります試みません。

4.  GpioClx パッシブで呼び出されるその他の割り込み関連および O 関連のコールバック関数では、このコールバック関数への呼び出しをシリアル化\_レベル。 そのため、コールバック関数は、銀行の待機をロックする必要があります試みません。

5.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックを取得し、関数が返された後にロックを解放します。 そのため、コールバック関数は、銀行の割り込みのロックを取得する必要があります試みません。

6.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックは取得しません。 GPIO コント ローラーのドライバーが必要になるすべての同期を提供する責任を負います。

## <a name="io-related-callback-functions"></a>O に関連するコールバック関数


データ I/O ピンとして構成されている GPIO ピンをサポートするためには、GPIO コント ローラーのドライバーは、一連のイベントのコールバック関数を介してこれらのピンの I/O 操作を管理するを実装します。 次の表では、中央の列は、GPIO コント ローラーのハードウェア レジスタ、メモリ マップされている場合に、関数が呼び出される IRQL を示します。 右端の列には、IRQL の場合は、レジスタのメモリ マッピングがないと、シリアル バスからアクセスする必要がありますが、関数が呼び出されることを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>IRQL if memory-mapped (MemoryMappedController = 1)</th>
<th>逐次的にアクセスする場合は、IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_ConnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)"><em>CLIENT_ConnectIoPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_DisconnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)"><em>CLIENT_DisconnectIoPins</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 1 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 2 を参照してください)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins)"><em>CLIENT_ReadGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)"><em>CLIENT_ReadGpioPinsUsingMask</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins)"><em>CLIENT_WriteGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)"><em>CLIENT_WriteGpioPinsUsingMask</em></a></p></td>
<td><p>DIRQL</p>
<p>(注 3 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 4 を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックは取得しません。 DIRQL で実行される関数の必要に応じて、コールバックで共有されているレジスタのアクセスを同期する場合、コールバック関数は、割り込みロックを取得できます。

2.  GpioClx パッシブで呼び出されるその他の割り込み関連および O 関連のコールバック関数では、このコールバック関数への呼び出しをシリアル化\_レベル。 そのため、コールバック関数は、銀行の待機をロックする必要があります試みません。

3.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックを取得し、関数が返された後にロックを解放します。 そのため、コールバック関数は、銀行の割り込みのロックを取得する必要があります試みません。

4.  GpioClx パッシブで呼び出されるその他の割り込み関連および O 関連のコールバック関数では、このコールバック関数への呼び出しをシリアル化\_レベル。 そのため、コールバック関数は、銀行の待機をロックする必要があります試みません。

## <a name="gpio-initialization-and-setup-related-callback-functions"></a>GPIO 初期化とセットアップに関連するコールバック関数


I/O を実行し、操作を中断する GPIO コント ローラーを設定するには、GPIO コント ローラーのドライバーは、一連のコント ローラーを初期化するためにイベントのコールバック関数を実装します。 次の表では、中央の列は、GPIO コント ローラーのハードウェア レジスタ、メモリ マップされている場合に、関数が呼び出される IRQL を示します。 右端の列には、IRQL の場合は、レジスタのメモリ マッピングがないと、シリアル バスからアクセスする必要がありますが、関数が呼び出されることを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>IRQL if memory-mapped (MemoryMappedController = 1)</th>
<th>逐次的にアクセスする場合は、IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller" data-raw-source="[&lt;em&gt;CLIENT_PrepareController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller)"><em>CLIENT_PrepareController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller" data-raw-source="[&lt;em&gt;CLIENT_ReleaseController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller)"><em>CLIENT_ReleaseController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller" data-raw-source="[&lt;em&gt;CLIENT_StartController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller)"><em>CLIENT_StartController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller" data-raw-source="[&lt;em&gt;CLIENT_StopController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller)"><em>CLIENT_StopController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information" data-raw-source="[&lt;em&gt;CLIENT_QueryControllerBasicInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)"><em>CLIENT_QueryControllerBasicInformation</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information" data-raw-source="[&lt;em&gt;CLIENT_QuerySetControllerInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)"><em>CLIENT_QuerySetControllerInformation</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 1 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 2 を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  を GpioClx がこれらのコールバック関数のいずれかを呼び出すと銀行の割り込みのロックは使用できません。 したがって、これらのコールバック関数は、銀行の割り込みのロックを取得する必要があります試みません。

2.  これらのコールバック関数が呼び出されたときに、GpioClx 銀行待機のロックは使用できません。 そのため、ドライバーは、これらのコールバック関数に同期する銀行待機ロックを取得する必要があります試みません。

## <a name="gpio-power-management-related-callback-functions"></a>GPIO 電源管理に関連するコールバック関数


デバイスの電源の状態を変更する GPIO コント ローラーを有効にするのには、GPIO コント ローラーのドライバーは、一連のイベントのコールバック関数を保存し、これらの変更中に、ハードウェアの設定を復元を実装します。 次の表では、中央の列は、GPIO コント ローラーのハードウェア レジスタ、メモリ マップされている場合に、関数が呼び出される IRQL を示します。 右端の列には、IRQL の場合は、レジスタのメモリ マッピングがないと、シリアル バスからアクセスする必要がありますが、関数が呼び出されることを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>IRQL if memory-mapped (MemoryMappedController = 1)</th>
<th>逐次的にアクセスする場合は、IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_RestoreBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)"><em>CLIENT_RestoreBankHardwareContext</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_SaveBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)"><em>CLIENT_SaveBankHardwareContext</em></a></p></td>
<td><p>DIRQL または HIGH_LEVEL</p>
<p>(詳しくは、ノートを参照してください)。</p></td>
<td><p>サポートされません。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

-   F 状態遷移の正規表現。DIRQL で GpioClx によって保持されている銀行割り込みロックでは、保存/復元のコールバック関数が呼び出されます。 したがって、どちらのコールバック関数は、銀行の割り込みのロックの取得をください。

<!-- -->

-   重要な F 状態遷移します。保存/復元のコールバックは、保存し、GPIO 状態を復元する電源エンジン プラグイン (PEP) が呼び出されたときに呼び出されます。 質の高い保存/復元のコールバック関数を呼び出す\_ディープ アイドル状態の遷移のシーケンスのプラットフォームで遅延が発生したが、アイドル状態にして最後のプロセッサのコンテキストでレベル。 したがって、どちらのコールバック関数は、銀行の割り込みのロックの取得をください。

F 状態の詳細については、次を参照してください。[コンポーネント レベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)します。 詳細については、PEP は、次を参照してください。 [ **PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)します。

## <a name="other-callback-functions"></a>その他のコールバック関数


コント ローラーに固有の操作をサポートするために GPIO コント ローラーを有効にする、GPIO コント ローラー用ドライバーを実装して、 [*クライアント\_ControllerSpecificFunction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)イベント コールバック関数。 次の表では、中央の列は、GPIO コント ローラーのハードウェア レジスタ、メモリ マップされている場合に、関数を呼び出す位置 IRQL を示します。 右端の列では、関数が呼び出される位置、レジスタがメモリ マップがなく、シリアル バスからアクセスする必要がある場合 IRQL を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コールバック関数</th>
<th>IRQL if memory-mapped (MemoryMappedController = 1)</th>
<th>逐次的にアクセスする場合は、IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function" data-raw-source="[&lt;em&gt;CLIENT_ControllerSpecificFunction&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)"><em>CLIENT_ControllerSpecificFunction</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 1 を参照してください)。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>(注 2 を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  GpioClx では、このコールバック関数を呼び出す前に、銀行の割り込みのロックは取得しません。 DIRQL で実行される関数の必要に応じて、コールバックで共有されているレジスタのアクセスを同期する場合、コールバック関数は、銀行の割り込みロックを取得できます。

2.  GpioClx パッシブで呼び出されるその他の割り込み関連および O 関連のコールバック関数では、このコールバック関数への呼び出しをシリアル化\_レベル。 そのため、コールバック関数は、銀行の待機をロックする必要があります試みません。

 

 




