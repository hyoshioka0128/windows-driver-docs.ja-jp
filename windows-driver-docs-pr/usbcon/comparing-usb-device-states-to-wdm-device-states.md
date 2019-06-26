---
Description: このトピックでは、ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定された USB デバイス電源状態を使用する WDM デバイスの状態について説明します。
title: USB デバイスの電源状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58ab116a5397dd9a151334fddd392f6f58d2f836
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381112"
---
# <a name="usb-device-power-states"></a>USB デバイスの電源状態


このトピックでは、ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定された USB デバイス電源状態を使用する WDM デバイスの状態について説明します。

USB デバイスの電源状態 (ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定) としては、次の 3 つの一般的なカテゴリに分類できます。

-   添付:デバイスが接続されているが、電源が完全には。
-   電源。デバイスの電源が入っている状態のいずれかが。既定値、アドレス、または構成します。
-   Suspended (中断): デバイスでは、アイドル状態と低電力で動作しています。

WDM power モデルで定義されているデバイスの電源状態と USB の標準で定義されているデバイスの電源状態の間の直接の相関関係はありません。 用語など*中断*と*アイドル*USB に非常に特定の意味がある仕様。 ただしこれらの用語は多くの場合、異なる方法で、モデルで使用 WDM 電源。 Windows クライアント ドライバーでは、"suspended"状態で、USB デバイスを配置できます。 詳細については、次を参照してください。 [USB セレクティブ サスペンド](usb-selective-suspend.md)します。 クライアント ドライバーをそのデバイスを中断する準備ができたら、バスの運転手がアイドル状態のことを指示します。 アイドル状態の要求の詳細については、次を参照してください。 [USB セレクティブ サスペンド](usb-selective-suspend.md)します。

デバイスの電源状態 WDM モデルに関するものです。

-   **D0** -動作状態。 デバイスの電源を完全にします。
-   **D1 または D2**の中間のスリープ状態です。 これらの状態は、リモート ウェイク アップ装備するデバイスをできるようにします。
-   **D3**の最下位のスリープ状態です。 状態のデバイスの**D3**リモート ウェイク アップ武装ことはできません。

WDM power モデル デバイスの電源状態の詳細については、次を参照してください。[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)します。

WDM power モデルという用語を使用する*取り組ま*のデバイスをリモート ウェイク アップします。 ハードウェア操作につながるを常にではありませんが、通常、ソフトウェアの操作は、取り組ま*を有効にする*USB デバイスにリモート ウェイク アップ機能。 リモート ウェイク アップのデバイスを準備する WDM ソフトウェア操作が待機ウェイク IRP ([**IRP\_MN\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake))。 この IRP の詳細については、次を参照してください。[サポート デバイスがあるウェイク アップ機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)します。

このソフトウェアの操作と、USB リモート ウェイク アップ機能を有効にする間のリレーションシップの詳細については、次を参照してください。 [USB デバイスのリモート ウェイク アップ](remote-wakeup-of-usb-devices.md)します。

このセクションには、次のサブセクションが含まれています。

-   [電源状態の非複合デバイスを変更します。](#changing-the-power-state-of-a-non-composite-device)
-   [複合デバイスの電源状態の変更](#changing-the-power-state-of-a-composite-device)
-   [関連トピック](#related-topics)

## <a name="changing-the-power-state-of-a-non-composite-device"></a>電源状態の非複合デバイスを変更します。


USB デバイスの電源ポリシー マネージャーは、デバイスの電源の状態を設定します。 WDM 電源を発行して、電源ポリシー マネージャーが電源の状態を設定 ([**IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) IRP します。 電源ポリシー マネージャーの詳細については、次を参照してください。[電源ポリシー所有権](https://docs.microsoft.com/windows-hardware/drivers/wdf/power-policy-ownership)します。

バス ドライバーによって実行されたアクションは、電源ポリシー マネージャーを要求するデバイスの電源のレベルに依存します。 電源の要求のセットのレベルごとに、バス ドライバーの動作を次に示します。

-   **D0**

    バス ドライバーは、次のタスクを実行します。

    1.  すべて upsteam USB ハブを電源と要求を受信する準備ができている保証します。
    2.  オフにすると、ポート、ポートが再開される\_中断機能、デバイスの USB ポートが中断されている場合。
    3.  完了状態で、デバイスのアイドル状態の IRP\_成功した場合、いずれかが保留中の場合。
    4.  装備された場合は、リモート ウェイクのデバイスをオンにします。
-   **D1 または D2**

    バス ドライバーは、次のタスクを実行します。

    1.  待機が IRP をスリープ解除する場合は、リモート ウェイク アップは、デバイスを準備 ([**IRP\_MN\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) が保留されています。
    2.  ポートを設定して、デバイスの USB ポートを中断します\_SUSPEND 機能。
-   **D3**

    バス ドライバーは、次のタスクを実行します。

    1.  ポートを設定して、デバイスの USB ポートを中断します\_SUSPEND 機能。
    2.  デバイスの待機ウェイク状態 IRP の完了\_POWER\_状態\_いずれかが保留中の場合は無効です。
    3.  デバイスのアイドル状態の IRP の完了 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification))の状態\_POWER\_状態\_いずれかが保留中の場合は無効です。

## <a name="changing-the-power-state-of-a-composite-device"></a>複合デバイスの電源状態の変更


複合デバイスのインターフェイス用のクライアント ドライバーでは、デバイス上の他のインターフェイス用のクライアント ドライバーと複合デバイスの電源状態を共有する必要があります。 そのためのインターフェイスのクライアント ドライバーは、デバイス上の他のインターフェイスに影響を与えずに、低電力状態に複合デバイスを配置できません。 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)インターフェイスのクライアント ドライバーに送信するとき、次の操作では、 [ **IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求。

-   **D0**

    バス ドライバーは、次のタスクを実行します。

    1.  すべて upsteam USB ハブを電源と要求を受信する準備ができている保証します。
    2.  オフにすると、ポート、ポートが再開される\_中断機能、デバイスの USB ポートが中断されている場合。
    3.  完了状態で、クライアント ドライバーのアイドル状態の IRP\_成功した場合、いずれかが保留中の場合。
-   **D1 または D2**

    バス ドライバーには、アクションはありません。

-   **D3**

    バス ドライバーは、次のタスクを実行します。

    1.  IRP をウェイク アップ クライアント ドライバーの待機が完了すると (IRP\_MN\_待機\_スリープ解除) 状態で\_POWER\_状態\_いずれかが保留中の場合は無効です。
    2.  クライアント ドライバーのアイドル状態の IRP の完了 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) の状態\_POWER\_状態\_いずれかが保留中の場合は無効です。

一般的な親ドライバーは、次の条件のいずれかが true の場合、デバイスの USB ポートを中断します。

-   システムは低電力状態に遷移中です。
-   クライアント ドライバーの複合デバイス上のすべての関数を選択的に開始した中断します。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  



