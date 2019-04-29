---
title: トランスポート バス ドライバーについてよく寄せられる質問
description: 次に一般的な質問、シナリオ、および問題ドライバー開発者が発生する可能性のある Bluetooth 機能をサポートするために、バス ドライバーを開発するときにします。
ms.assetid: 7189EB3B-E071-4145-8308-EFA6D4E89D4B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 172d5d753747d46a60c1b563542d588c1eb31021
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328185"
---
# <a name="transport-bus-driver-faq"></a>トランスポート バス ドライバーについてよく寄せられる質問


次に一般的な質問、シナリオ、および問題ドライバー開発者が発生する可能性のある Bluetooth 機能をサポートするために、バス ドライバーを開発するときにします。

## <a name="span-idmyserialbusdriverencounteredsomeerrorwhatdoesitmeanspanspan-idmyserialbusdriverencounteredsomeerrorwhatdoesitmeanspanmy-serial-bus-driver-encountered-some-error-what-does-it-mean"></a><span id="my_serial_bus_driver_encountered_some_error._what_does_it_mean_"></span><span id="MY_SERIAL_BUS_DRIVER_ENCOUNTERED_SOME_ERROR._WHAT_DOES_IT_MEAN_"></span>シリアル バス ドライバーには、いくつかのエラーが発生しました。 それはどういう意味ですか。


10 ~ 49 のコード:[デバイス マネージャーによって生成されたエラー コードの説明](http://support.microsoft.com/kb/310123)します。

コード 51:シリアル バス ドライバーに依存するコント ローラー ドライバー (ACPI テーブルで定義) された場合は、システムは、シリアル バス ドライバーを読み込むなりますがいない取得開始依存に関連するドライバーのすべてが正常に開始されるまでです。 コント ローラー ドライバーが存在しないまたは、読み込まれていませんが正常に 51 にコードのエラーがトリガーされた場合。

52 をコード署名されていないドライバーを = です。

ドライバーの署名は、これらのトピックで詳しく説明します。

-   [ドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff544865)
-   [Windows のドライバー署名の要件](https://msdn.microsoft.com/windows/hardware/gg487317)

## <a name="span-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanspan-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanspan-idwhyismyserialbusdrivernotgettinganyioctlsfromthebluetoothcorestackspanwhy-is-my-serial-bus-driver-not-getting-any-ioctls-from-the-bluetooth-core-stack"></a><span id="Why_is_my_serial_bus_driver_not_getting_any_IOCTLs_from_the_Bluetooth_core_stack_"></span><span id="why_is_my_serial_bus_driver_not_getting_any_ioctls_from_the_bluetooth_core_stack_"></span><span id="WHY_IS_MY_SERIAL_BUS_DRIVER_NOT_GETTING_ANY_IOCTLS_FROM_THE_BLUETOOTH_CORE_STACK_"></span>理由には、シリアル バス ドライバーが供給されていない任意の Ioctl Bluetooth core スタックからでしょうか。


シリアル バス ドライバーは、アイドル状態の機能を有効になっているが、処理のメカニズムと各サブトピック セクションで説明した電源管理を実装していないが可能性があります。 このような状況で Bluetooth HID デバイス (マウスやキーボード) は、スタック (D0 を D2) からのスリープを解除できません。 Bluetooth の基本的な機能と電源管理の処理のメカニズムが実装されているまでこのアイドル状態の機能をオフにすることをお勧めします。

## <a name="span-idaretherebluetoothwindowslogotestsspanspan-idaretherebluetoothwindowslogotestsspanspan-idaretherebluetoothwindowslogotestsspanare-there-bluetooth-windows-logo-tests"></a><span id="Are_there_Bluetooth_Windows_Logo_Tests_"></span><span id="are_there_bluetooth_windows_logo_tests_"></span><span id="ARE_THERE_BLUETOOTH_WINDOWS_LOGO_TESTS_"></span>Bluetooth の Windows ロゴのテストはありますか。


Windows HCK (ハードウェア認定キット) には、一連認定を受けるに渡す必要がある特定の Bluetooth テストにはが含まれています。 Bluetooth ドライバー開発者は、開発時に、ドライバーが認定を受けるしは適切なをサポートするためにそれらを渡しますを確実にこれらのテストを実行する必要があります。

## <a name="span-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanspan-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanspan-idshoulduartsettingsbepreservedandrestoredamongthedifferentpowerstatetransitionsspanshould-uart-settings-be-preserved-and-restored-among-the-different-power-state-transitions"></a><span id="Should_UART_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="should_uart_settings_be_preserved_and_restored_among_the_different_power_state_transitions_"></span><span id="SHOULD_UART_SETTINGS_BE_PRESERVED_AND_RESTORED_AMONG_THE_DIFFERENT_POWER_STATE_TRANSITIONS_"></span>必要があります UART 設定空白を保持し、別の電源の状態遷移の間で復元しますか。


Bluetooth トランスポート ドライバーを認識しており、リモート UART コント ローラーの設定を制御するため (電源を入れた後その設定を含む)、Bluetooth トランスポート ドライバーがリセット両方のリモートおよびローカル UART コント ローラーの状態に入る前に電源は失われる可能性があります。 そのため、電源が復元されたら、リモート UART (Bluetooth 側) とローカル UART (ホスト側) コント ローラーの両方の設定は同期のようにできます。UART ドライバーでは、ローカル UART controller のみを制御し、電源を切る前にその設定を復元する負担になります。 Bluetooth のトランスポート ドライバーを (UART ドライバーは、最初に、ACPI テーブルを使用して設定) してから、電源設定に関する UART ドライバーのクエリを実行できるはもキャッシュし、一部 Dx 状態に移行する場合にも設定は。

## <a name="span-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanspan-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanspan-idwhathappensifthebusdriverreceivesawakenotificationwhilethestackisintheprocessofenteringd2spanwhat-happens-if-the-bus-driver-receives-a-wake-notification-while-the-stack-is-in-the-process-of-entering-d2"></a><span id="What_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_D2_"></span><span id="what_happens_if_the_bus_driver_receives_a_wake_notification_while_the_stack_is_in_the_process_of_entering_d2_"></span><span id="WHAT_HAPPENS_IF_THE_BUS_DRIVER_RECEIVES_A_WAKE_NOTIFICATION_WHILE_THE_STACK_IS_IN_THE_PROCESS_OF_ENTERING_D2_"></span>D2 を入力するプロセスでは、スタックは、バス ドライバーがウェイク アップ通知を受信するとどうなりますか。


このような状況で、バス ドライバーを D2 の切り替えを完了し、スリープ解除メカニズムに進みます。 (例: スリープ解除要求はキューにして D2 の移行が完了した後にのみ、ウェイク アップ プロセスを開始) は、この同期を行うには、シリアル バス ドライバーが必要です。

## <a name="span-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanspan-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanspan-idhowshouldabusdriveridentifyitsacpiresourceofmultipleoccurrencessuchasmultiplegpiosspanhow-should-a-bus-driver-identify-its-acpi-resource-of-multiple-occurrences-such-as-multiple-gpios"></a><span id="How_should_a_bus_driver_identify_its_ACPI_resource_of_multiple_occurrences__such_as_multiple_GPIOs_"></span><span id="how_should_a_bus_driver_identify_its_acpi_resource_of_multiple_occurrences__such_as_multiple_gpios_"></span><span id="HOW_SHOULD_A_BUS_DRIVER_IDENTIFY_ITS_ACPI_RESOURCE_OF_MULTIPLE_OCCURRENCES__SUCH_AS_MULTIPLE_GPIOS_"></span>バス ドライバーが複数 GPIOs など、複数回出現の ACPI リソースを識別する方法はありますか


GPIO のリソースにタグ付けする方法はありませんか、それ以外の場合。 これは、ため、リソースの順序が重要です。 デバイス ドライバーは、規則を確立する必要があります (例: リストに表示される最初の GPIO リソースは BT\_ウェイク アップし、2 つ目に表示されるはホストの\_WAKE)。

 

 





