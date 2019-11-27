---
title: 省略可能および必須の GPIO コールバック関数
description: 汎用 i/o (GPIO) コントローラードライバーは、GPIO_CLX_RegisterClient メソッドを呼び出して、GPIO framework 拡張機能 (GpioClx) のクライアントとして登録します。
ms.assetid: 2F126431-13AB-4E3F-9E5E-56DC7D9AF024
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54105426a2d003334c99195436841fdbdf7af492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824936"
---
# <a name="optional-and-required-gpio-callback-functions"></a>省略可能および必須の GPIO コールバック関数


汎用 i/o (GPIO) コントローラードライバーは、gpio フレームワーク拡張機能 (GpioClx) のクライアントとして登録するために、 [**gpio\_CLX\_RegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)メソッドを呼び出します。 この呼び出しの間に、ドライバーは、ドライバーによって実装されているイベントコールバック関数のリストを指定する登録パケットを GpioClx に渡します。 GpioClx は、これらのコールバック関数を呼び出して、GPIO コントローラーハードウェアを構成し、i/o 操作を実行し、割り込みを管理します。 GpioClx では、特定のコールバック関数を実装するために、GPIO コントローラードライバーが必要ですが、他のコールバック関数のサポートは省略可能です。

登録パケットは、[**パケット構造\_の GPIO\_クライアント\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_gpio_client_registration_packet)パケットです。 GPIO コントローラードライバーが特定のコールバック関数を実装している場合は、そのコールバック関数への関数ポインターを、この構造体の対応するメンバーに書き込みます。 または、特定のコールバック関数がサポートされていないことを示すために、ドライバーは、対応するメンバーに NULL を書き込みます。

次のコールバック関数を登録パケットに含める必要があります。

[*クライアント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller)
[*クライアント\_Querycontroller Basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)
[*Client\_Startcontroller*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)
[*CLIENT\_stopcontroller*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)
[*クライアント\_ReleaseController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller) 。前の一覧のコールバック関数が見つからない場合 (つまり、登録パケット内の対応する関数ポインターが NULL の場合)、 **GPIO\_clx\_registerclient**メソッドは失敗します。.

Gpio i/o ピンへの読み取りまたは書き込みをサポートするために、GPIO コントローラードライバーは必要ありません。これは、データ入力またはデータ出力として構成されているピンです。 (I/o ピンがない GPIO コントローラーは、周辺機器からの割り込み要求を引き続きリレーできます)。ただし、登録パケットに次のいずれかの i/o 関連コールバック関数が含まれる場合、パケットには次のコールバック関数の両方が含まれている必要があります。

[*クライアント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)
[*クライアント\_Dis/tiopins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)に加えて、登録パケットに前の一覧に2つのコールバック関数が含まれている場合、ドライバーは、さらに、GPIO i/o ピンからの読み取りをサポートする必要があります。GPIO i/o ピンへの書き込み、またはその両方。 具体的には、登録パケットには、次の一覧にコールバック関数が少なくとも1つ含まれている必要があります。

[*クライアント\_ReadGpioPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)または[*client\_ReadGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)
[*Client\_writegpiopins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)または[*client\_WriteGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)をサポートするドライバーは、前の一覧の2つの*クライアント\_ReadGpioPins*Xxx コールバック関数。 書き込みをサポートするドライバーは、上記の一覧にある2つの*クライアント\_writの*両方のコールバック関数のいずれかを実装する必要があります。

クライアント *\_ReadGpioPinsUsingMask*、 *client\_WriteGpioPinsUsingMask*、またはその両方を実装するドライバーでは、クライアントによって提供されるデバイス情報に**FormatIoRequestsAsMasks**フラグビットを設定する必要があり[ *\_Queryコントローラー Basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック関数。 *クライアント\_ReadGpioPins*、 *Client\_writegpiopins*、またはその両方を実装するドライバーでは、このフラグビットを設定しないようにする必要があります。 詳細については、「 [**CLIENT\_CONTROLLER\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)の**Flags**メンバーの説明」を参照してください。

Gpio の割り込みをサポートするために、GPIO コントローラードライバーは必要ありません。 ただし、登録パケットに次の割り込み関連のコールバック関数のいずれかが含まれている場合、パケットには次のコールバック関数がすべて含まれている必要があります。

クライアント[ *\_enableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)
[*クライアント\_Disableinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)
[*クライアント\_マスク割り込み*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
[*クライアント\_queryactiveinterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
[*client\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)割り込みのマスクをサポートするドライバーは、*クライアント\_の maskinterrupt*コールバック関数を実装する必要があります。 アクティブな割り込みのクエリをサポートするドライバーは、*クライアント\_QueryActiveInterrupts*コールバック関数を実装する必要があります。

[*クライアント\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)コールバック関数は特殊なケースです。 GPIO コントローラーハードウェアが読み取り時にアクティブな割り込みを自動的にクリアする場合、*クライアント\_ClearActiveInterrupts*関数は必要ありません。また、登録パケット内の対応する関数ポインターを NULL に設定する必要があります。 ただし、アクティブな割り込みが読み込まれたときに自動的にクリアされない場合や、前の一覧の割り込みに関連するコールバック関数が登録パケットに指定されている場合は、*クライアント\_ClearActiveInterrupts*関数がである必要があります。パケットに含まれています。 ハードウェアが読み取り時にアクティブな割り込みを自動的にクリアすることを示すために、ドライバーは、クライアントによって提供されるデバイス情報に**ActiveInterruptsAutoClearOnRead**フラグビットを設定し[ *\_Queryコントローラー Basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)コールバック関数。 詳細については、「 [**CLIENT\_CONTROLLER\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)の**Flags**メンバーの説明」を参照してください。

GPIO コントローラードライバーで GPIO 割り込みがサポートされている場合、登録パケットはオプションとして次のコールバック関数を含むことができます。

[*クライアント\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)GpioClx は、Windows 8.1 で始まる*クライアント\_QueryEnabledInterrupts*関数をサポートしています。

[コンポーネントレベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)をサポートするドライバーは、次のコールバック関数の両方を実装する必要があります。

[*クライアント\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)
[*client\_SaveBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)がハードウェアがコンポーネントレベルの電源管理をサポートしていることを示すために、ドライバーは**BankIdlePowerMgmtSupported**フラグを設定します。クライアントによって提供されるデバイス情報のビットは、 [*Queryコントローラー basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) callback 関数\_ます。 詳細については、「 [**CLIENT\_CONTROLLER\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)の**Flags**メンバーの説明」を参照してください。

[*クライアント\_Preprocessコントローラー interrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)、 [*client\_ReconfigureInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)、および[*client\_コントローラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)のコールバック関数は省略可能であり、gpioclx to アドレスによってサポートされています。一部の GPIO controller 実装におけるハードウェア固有の問題。 特別な要件を持つ GPIO controller ドライバーのみが、これらの機能を実装します。

 

 




