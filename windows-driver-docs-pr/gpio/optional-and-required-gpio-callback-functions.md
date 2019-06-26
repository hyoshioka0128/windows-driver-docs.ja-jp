---
title: 省略可能および必須の GPIO コールバック関数
description: 汎用入出力 (GPIO) コント ローラーのドライバーでは、GPIO フレームワーク拡張機能 (GpioClx) のクライアントとして登録する GPIO_CLX_RegisterClient メソッドを呼び出します。
ms.assetid: 2F126431-13AB-4E3F-9E5E-56DC7D9AF024
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f481b34385b8bdd6cf83bae94457477578307ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383416"
---
# <a name="optional-and-required-gpio-callback-functions"></a>省略可能および必須の GPIO コールバック関数


汎用の I/O (GPIO) コント ローラー ドライバーは呼び出し、 [ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient) GPIO フレームワーク拡張機能 (GpioClx) のクライアントとして登録します。 この呼び出し中に、ドライバーはドライバーによって実装されているイベントのコールバック関数の一覧を示す GpioClx に登録パケットを渡します。 GpioClx は、GPIO コント ローラーのハードウェア構成、I/O 操作を実行および割り込みを管理するこれらのコールバック関数を呼び出します。 GpioClx では、GPIO コント ローラーのドライバーを特定のコールバック関数の実装が他のコールバック関数は省略可能なサポートが必要です。

登録のパケットが、 [ **GPIO\_クライアント\_登録\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_gpio_client_registration_packet)構造体。 GPIO コント ローラーのドライバーでは、特定のコールバック関数を実装する場合にこの構造体の対応するメンバーにそのコールバック関数、関数ポインターを書き込みます。 または、特定のコールバック関数がサポートされていないことを示す場合、ドライバーでは、対応するメンバーに NULL を書き込みます。

登録パケットでは、次のコールバック関数を含める必要があります。

[*クライアント\_PrepareController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller)
[*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) 
 [*クライアント\_StartController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller)
[*クライアント\_StopController* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller) 
 [*クライアント\_ReleaseController* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller) (関数の登録でポインターを対応する場合は、上記のコールバック関数が不足しているかどうかパケットが NULL)、 **GPIO\_CLX\_RegisterClient**メソッドは失敗します。

GPIO コント ローラーのドライバーがからの読み取りまたは書き込み I/O の GPIO ピンをサポートする必要はありませんはデータ入力またはデータとして構成されているピンを出力します。 (なし I/O ピン GPIO コント ローラーがまだ周辺機器からの割り込み要求をリレー。)ただし、登録パケットには、次の O に関連するコールバック関数のいずれかが含まれている場合、パケットは、次のコールバック関数のどちらもデータを含める必要があります。

[*クライアント\_ConnectIoPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)
[*クライアント\_DisconnectIoPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)さらに、登録のパケットが含まれている場合、上記の 2 つのコールバック関数、ドライバーする必要がありますさらにサポートする I/O の GPIO ピンの場合、またはその両方への書き込みの I/O の GPIO ピンからの読み取り。 具体的には、登録パケットは、次の一覧に少なくとも 1 つのコールバック関数を含める必要があります。

[*クライアント\_ReadGpioPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins)または[*クライアント\_ReadGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)
[*クライアント\_WriteGpioPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins)または[*クライアント\_WriteGpioPinsUsingMask* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)読み取りをサポートしているドライバーが 1 つを実装する必要があります、2 つ*クライアント\_ReadGpioPins*Xxx コールバック関数が、上記の一覧にします。 書き込みをサポートするドライバーは、2 つのいずれかを実装する必要があります*クライアント\_WriteGpioPins*Xxx コールバック関数が、上記の一覧にします。

実装するドライバー*クライアント\_ReadGpioPinsUsingMask*、*クライアント\_WriteGpioPinsUsingMask*、または両方を設定する必要があります、 **FormatIoRequestsAsMasks**フラグのビットによって提供されるデバイス情報、 [*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック関数。 実装するドライバー*クライアント\_ReadGpioPins*、*クライアント\_WriteGpioPins*、または両方、このフラグのビットを設定する必要があります。 詳細については、の説明を参照して、**フラグ**メンバー [**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)します。

GPIO コント ローラーのドライバーは、GPIO 割り込みをサポートする必要はありません。 ただし、登録のパケットには、次の割り込みに関連するコールバック関数のいずれかが含まれている場合、パケットはすべて、次のコールバック関数のデータを含める必要があります。

[*クライアント\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)
[*クライアント\_DisableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) 
 [ *クライアント\_MaskInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
[*クライアント\_QueryActiveInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts) 
 [*クライアント\_UnmaskInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)割り込みのマスクをサポートしているドライバーを実装する必要があります、*クライアント\_MaskInterrupts*コールバック関数。 アクティブな割り込みのクエリをサポートするドライバーを実装する必要があります、*クライアント\_QueryActiveInterrupts*コールバック関数。

[*クライアント\_ClearActiveInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)コールバック関数は、特殊なケースです。 GPIO コント ローラーのハードウェアが自動的に読み取られるときにアクティブな割り込みがオフの場合、*クライアント\_ClearActiveInterrupts*関数は必要ありませんし、登録に対応する関数ポインターパケットは、NULL に設定する必要があります。 登録のパケットで読み取られるとき、アクティブな割り込みが自動的にクリアされませんし、上記の一覧で、割り込みに関連するコールバックが機能する場合を指定するただし、*クライアント\_ClearActiveInterrupts*パケットで関数を含める必要があります。 読み取られるとき、ドライバー、ハードウェアがそのアクティブな割り込みを自動的に消去されるかを示す設定、 **ActiveInterruptsAutoClearOnRead**フラグのビットによって提供されるデバイス情報、 [ *クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック関数。 詳細については、の説明を参照して、**フラグ**メンバー [**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)します。

GPIO コント ローラーのドライバーでは、GPIO 割り込みをサポートする場合、登録パケット含めることができます、オプションとして、次のコールバック関数。

[*クライアント\_QueryEnabledInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) GpioClx サポート、*クライアント\_QueryEnabledInterrupts*関数が Windows 8.1 以降します。

サポートするドライバー[コンポーネント レベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)次のコールバック関数の両方を実装する必要があります。

[*クライアント\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)
[*クライアント\_SaveBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)いることを示すハードウェアコンポーネント レベルの電源管理、ドライバーのセットをサポート、 **BankIdlePowerMgmtSupported**フラグのビットによって提供されるデバイス情報、 [*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック関数。 詳細については、の説明を参照して、**フラグ**メンバー [**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)します。

[*クライアント\_PreProcessControllerInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)、 [*クライアント\_ReconfigureInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)と[*クライアント\_ControllerSpecificFunction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)コールバック関数は省略可能で、いくつかの GPIO コント ローラーのハードウェアに固有の問題に対処する GpioClx でサポートされます。実装。 特別な要件に GPIO コント ローラー ドライバーだけでは、これらの関数を実装します。

 

 




