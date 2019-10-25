---
title: GPIO コントローラーの要件チェック リスト
description: このトピックでは、Windows に公開されている General Purpose IO (GPIO) コントローラーデバイスのハードウェア、ファームウェア、およびソフトウェアの要件について説明します。
ms.assetid: 8097F391-ABF0-44A6-94D2-243AFBA3F984
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57bf8b8fa76b1c255398f0d31fb0411b51e3602f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834480"
---
# <a name="gpio-controller-requirements-checklist"></a>GPIO コントローラーの要件チェック リスト


このトピックでは、Windows に公開されている General Purpose IO (GPIO) コントローラーデバイスのハードウェア、ファームウェア、およびソフトウェアの要件について説明します。

## <a name="gpio-controller-hardware-requirements"></a>GPIO コントローラーのハードウェア要件


-   GPIO コントローラーは SoC (SPB バスでは接続されていません) に統合されています。

    エミュレートされた ActiveBoth の信頼性が向上します。

-   レベルモードの割り込みがサポートされています。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

-   高と低の両方の割り込み polarities がサポートされています。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

-   割り込み極性は、実行時に再プログラミングできます。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

## <a name="gpio-controller-firmware-requirements"></a>GPIO コントローラーファームウェアの要件


-   GPIO controller \_CRS には、コントローラー内のすべてのピンバンクのすべてのリソースが含まれます。
-   GPIO コントローラー \_CRS リソースの順序付けによって、銀行からシステムへの割り込みマッピングが提供されます。
-   \_AEI メソッド、およびイベントメソッド (\_Exx、\_Lxx または \_.EVT) は、GPIO シグナル状態の ACPI イベントに対して存在します。
-   コントローラーに接続されているいずれかの割り込みが、ロジック不足ではなくアサートされた論理高である場合、GPIO コントローラー \_DSM が含まれています。
-   \_REG が領域ハンドラーを使用できないことを示している場合は、各 GPIO コントローラーに \_REG メソッドを実装し、GeneralPurposeIO OpRegions の使用を禁止します。
-   Debounce タイムアウトは、debounce を必要とするすべての割り込みの GPIOInt リソース記述子に含まれています。

## <a name="gpio-controller-driver-requirements"></a>GPIO コントローラードライバーの要件


-   GpioClx と GPIO controller ドライバーの間のインターフェイスのバージョン2をサポートします。

    -   [*クライアント\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)コールバック関数を実装します。 これは、割り込みストームの診断に役立ちます。
    -   **BankIdlePowerMgmtSupported**フラグが[**コントローラー\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)の構造体で設定されている場合、GPIO コントローラードライバーは[*クライアント\_SaveBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)とクライアントを実装する必要があり[ *\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)コールバック関数とこれらの関数は、割り込みのマスクされた状態やマスクされていない状態など、銀行のコンテキストを適切に保存/復元する必要があります。 この関数が呼び出されたときに割り込みが切断されることは保証されていませんが、まだ接続されている場合はマスクされることが保証されます。
    -   **DeviceIdlePowerMgmtSupported**フラグが**コントローラー\_基本\_情報**の構造体で設定されている場合は、[*クライアント\_Startcontroller*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)と[*クライアント\_stopcontroller*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)コールバック関数を指定する必要があります。割り込みのマスクされたまたはマスク解除された状態を含め、すべての銀行のコンテキストを適切に保存/復元します。 この関数が呼び出されたときに割り込みが切断されることは保証されていませんが、まだ接続されている場合はマスクされることが保証されます。
-   **コントローラー\_基本\_情報**構造体に**EmulateDebouncing**フラグを設定します。 これにより、割り込みが静電気放電の対象となるデバイス (ボタン、プラグなど) に対するノイズ電磁波耐性が大幅に増加します。
-   **コントローラー\_基本\_情報**構造体に**EmulateActiveBoth**フラグを設定し、 [*CLIENT\_ReconfigureInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt) callback 関数を実装します。 これにより、両方の割り込みの信頼性の高いエッジ検出が実現します。

 

 




