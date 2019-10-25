---
title: 割り込み関連のコールバック
description: オプションとして、汎用 i/o (GPIO) コントローラーのドライバーは、GPIO 割り込みをサポートすることができます。
ms.assetid: 638B52A0-CB8D-4A79-B7D1-ED2474E46DAE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac79e60cda3c81ae5835cb8d748ad1450a84cf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824940"
---
# <a name="interrupt-related-callbacks"></a>割り込み関連のコールバック


オプションとして、汎用 i/o (GPIO) コントローラーのドライバーは、GPIO 割り込みをサポートすることができます。 Gpio 割り込みをサポートするために、GPIO コントローラードライバーは、これらの割り込みを管理するためのコールバック関数のセットを実装します。 ドライバーには、そのドライバーが GPIO framework extension (GpioClx) のクライアントとして登録するときに提供される、登録パケット内のこれらのコールバック関数へのポインターが含まれています。 この登録パケットの詳細については、「 [**GPIO\_CLIENT\_registration\_packet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_gpio_client_registration_packet)」を参照してください。

原則として、チップ (SoC) チップ上のシステムに統合されている GPIO コントローラーには、SoC チップのプロセッサが直接アクセスできるメモリマップトハードウェアレジスタがあります。 ただし、次の図に示すように、別の GPIO コントローラーデバイスがシリアルバスを介して SoC チップに外部接続されている可能性があります。

![統合された gpio コントローラーと外部 gpio コントローラー](images/gpioconnects.png)

この図では、外部 GPIO コントローラーが I ² C バスに接続されています。 このバスは、SoC チップの統合された部分である I ² C バスコントローラーによって制御されます。 外部 GPIO コントローラーからの割り込み要求行は、統合された GPIO コントローラーのピンに接続されています。 [Gpioclx DDI](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-ddi)は、この例の統合された gpio コントローラーと外部 gpio コントローラーの両方に対応できます。

GPIO コントローラーデバイスがメモリにマップされている場合、GPIO コントローラードライバーは DIRQL のコントローラーのハードウェアレジスタに直接アクセスできます。 ただし、GPIO コントローラーが直列に接続されている場合、GPIO コントローラードライバーは、「[受動レベル isr](https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs)」で説明されているように、IRQL = パッシブ\_レベルでのみハードウェアレジスタにアクセスできます。

メモリマップトハードウェアレジスタがある GPIO コントローラーのドライバーは、ドライバーが GpioClx に提供するデバイス情報に**MemoryMappedController**フラグビットを設定する必要があります。 そうしないと、GpioClx はハードウェアレジスタがメモリマップトではないと想定し、ドライバーは IRQL = パッシブ\_レベルでのみこれらのレジスタにアクセスできます。 このフラグビットの詳細については、「 [**CONTROLLER\_ATTRIBUTE\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_controller_attribute_flags)」を参照してください。

GpioClx は、GPIO コントローラーからの割り込み要求を処理するための割り込みサービスルーチン (ISR) を実装します。 この ISR は、次の割り込みに関連するコールバック関数を呼び出します。

クライアント[ *\_clearactiveinterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
[*Client\_Maskinterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
[*client\_Queryactiveinterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
[*client\_queryactiveinterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)
[*クライアント\_UnmaskInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)これらの関数は、GpioClx の ISR が dirql またはパッシブ\_レベルで実行されるかどうかに応じて、DIRQL またはパッシブ\_レベルで呼び出されます。 ISR は、 **MemoryMappedController** = 1 の場合は Dirql、 **MemoryMappedController** = 0 の場合はパッシブ\_レベルでこれらの関数を呼び出します。 どちらの場合も、ISR は自動的にコールバックをシリアル化して、これらの関数のいずれかの呼び出しが、これらの関数の別の呼び出しの途中で発生しないようにします。

GPIO framework 拡張機能は、 **MemoryMappedController** フラグが設定されているかどうかに関係なく、パッシブ\_レベルでのみ、次の割り込み関連のコールバック関数を呼び出します。

[*クライアント\_disableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)
[*Client\_enableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt) **MemoryMappedController**フラグが設定されていない場合は、割り込みに関連するすべてのコールバック関数がパッシブ\_レベルで呼び出されます。 GpioClx はこれらの関数の呼び出しを自動的にシリアル化して、これらの関数のいずれかの呼び出しの途中でこれらの関数を呼び出すことができないようにします。

ただし、 **MemoryMappedController**フラグが設定されている場合、*クライアント\_enableinterrupt*関数と*クライアント\_disableinterrupt* functions は明示的に割り込みの有効化と無効化の操作を gpioclx に同期する必要があります。ISR: DIRQL で、他の4つの割り込み関連のコールバック関数を呼び出します。

通常、他の<em>クライアント\_</em>Xxx コールバック関数 (名前に "*interrupt*" が含まれていない) は割り込みに関連する処理を実行しないため、GpioClx ISR と同期する必要はありません。 ただし、これらの関数のいずれかがパッシブ\_レベルで呼び出された場合に、DIRQL で割り込みに関連する関数によってアクセスされる割り込み設定にアクセスするコードが含まれていると、このコードを ISR に同期する必要があります。

割り込み同期をサポートするために、GpioClx は一連の割り込みロックを実装します。 パッシブ\_レベルで実行されるコールバック関数は、 [**gpio\_clx\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)メソッドを呼び出して割り込みロックを取得し、 [**gpio\_Clx\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)メソッドを呼び出して、制限. 関数が割り込みロックを保持している場合、GpioClx ISR を実行できず、この ISR は割り込みに関連するコールバック関数を呼び出すことができません。 GPIO 割り込みが適時に処理されるようにするには、ドライバーが必要以上に割り込みロックを保持する必要があります。

詳細については、「 [GPIO Controller ドライバーの割り込み同期](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers)」を参照してください。

 

 




