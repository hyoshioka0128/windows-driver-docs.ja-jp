---
Description: This topic describes the WDM device states to use for USB device power states as specified in section 9.1 of the Universal Serial Bus 2.0 specification.
title: USB デバイスの電源状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1d086417d1f4898c2bc80dfb62a1f3591d20d93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569942"
---
# <a name="usb-device-power-states"></a>USB デバイスの電源状態


このトピックでは、ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定された USB デバイス電源状態を使用する WDM デバイスの状態について説明します。

USB デバイスの電源状態 (ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定) としては、次の 3 つの一般的なカテゴリに分類できます。

-   添付:デバイスが接続されているが、電源が完全には。
-   電源。デバイスの電源が入っている状態のいずれかが。既定値、アドレス、または構成します。
-   中断。デバイスでは、アイドル状態と低電力で動作しています。

WDM power モデルで定義されているデバイスの電源状態と USB の標準で定義されているデバイスの電源状態の間の直接の相関関係はありません。 用語など*中断*と*アイドル*USB に非常に特定の意味がある仕様。 ただしこれらの用語は多くの場合、異なる方法で、モデルで使用 WDM 電源。 Windows クライアント ドライバーでは、"suspended"状態で、USB デバイスを配置できます。 詳細については、[USB セレクティブ サスペンド](usb-selective-suspend.md)を参照してください。 クライアント ドライバーをそのデバイスを中断する準備ができたら、バスの運転手がアイドル状態のことを指示します。 アイドル状態の要求の詳細については、[USB セレクティブ サスペンド](usb-selective-suspend.md)を参照してください。

デバイスの電源状態 WDM モデルに関するものです。

-   **D0** -動作状態。 デバイスの電源を完全にします。
-   **D1 または D2**の中間のスリープ状態です。 これらの状態は、リモート ウェイク アップ装備するデバイスをできるようにします。
-   **D3**の最下位のスリープ状態です。 状態のデバイスの**D3**リモート ウェイク アップ武装ことはできません。

WDM power モデル デバイスの電源状態の詳細については、[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)を参照してください。

WDM power モデルという用語を使用する*取り組ま*のデバイスをリモート ウェイク アップします。 ハードウェア操作につながるを常にではありませんが、通常、ソフトウェアの操作は、取り組ま*を有効にする*USB デバイスにリモート ウェイク アップ機能。 リモート ウェイク アップのデバイスを準備する WDM ソフトウェア操作が待機ウェイク IRP ([**IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766))。 この IRP の詳細については、[サポート デバイスがあるウェイク アップ機能](https://msdn.microsoft.com/library/windows/hardware/ff563907)を参照してください。

このソフトウェアの操作と、USB リモート ウェイク アップ機能を有効にする間のリレーションシップの詳細については、[USB デバイスのリモート ウェイク アップ](remote-wakeup-of-usb-devices.md)を参照してください。

このセクションには、次のサブセクションが含まれています。

-   [電源状態の非複合デバイスを変更します。](#changing-the-power-state-of-a-non-composite-device)
-   [複合デバイスの電源状態の変更](#changing-the-power-state-of-a-composite-device)
-   [関連トピック](#related-topics)

## <a name="changing-the-power-state-of-a-non-composite-device"></a>電源状態の非複合デバイスを変更します。


USB デバイスの電源ポリシー マネージャーは、デバイスの電源の状態を設定します。 WDM 電源を発行して、電源ポリシー マネージャーが電源の状態を設定 ([**IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)) IRP します。 電源ポリシー マネージャーの詳細については、[電源ポリシー所有権](https://msdn.microsoft.com/library/windows/hardware/ff544518)を参照してください。

バス ドライバーによって実行されたアクションは、電源ポリシー マネージャーを要求するデバイスの電源のレベルに依存します。 電源の要求のセットのレベルごとに、バス ドライバーの動作を次に示します。

-   **D0**

    バス ドライバーは、次のタスクを実行します。

    1.  すべて upsteam USB ハブを電源と要求を受信する準備ができている保証します。
    2.  オフにすると、ポート、ポートが再開される\_中断機能、デバイスの USB ポートが中断されている場合。
    3.  完了状態で、デバイスのアイドル状態の IRP\_成功した場合、いずれかが保留中の場合。
    4.  装備された場合は、リモート ウェイクのデバイスをオンにします。
-   **D1 または D2**

    バス ドライバーは、次のタスクを実行します。

    1.  待機が IRP をスリープ解除する場合は、リモート ウェイク アップは、デバイスを準備 ([**IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766)) が保留されています。
    2.  ポートを設定して、デバイスの USB ポートを中断します\_SUSPEND 機能。
-   **D3**

    バス ドライバーは、次のタスクを実行します。

    1.  ポートを設定して、デバイスの USB ポートを中断します\_SUSPEND 機能。
    2.  デバイスの待機ウェイク状態 IRP の完了\_POWER\_状態\_いずれかが保留中の場合は無効です。
    3.  デバイスのアイドル状態の IRP の完了 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270))の状態\_POWER\_状態\_いずれかが保留中の場合は無効です。

## <a name="changing-the-power-state-of-a-composite-device"></a>複合デバイスの電源状態の変更


複合デバイスのインターフェイス用のクライアント ドライバーでは、デバイス上の他のインターフェイス用のクライアント ドライバーと複合デバイスの電源状態を共有する必要があります。 そのためのインターフェイスのクライアント ドライバーは、デバイス上の他のインターフェイスに影響を与えずに、低電力状態に複合デバイスを配置できません。 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)インターフェイスのクライアント ドライバーに送信するとき、次の操作では、 [ **IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)要求。

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
    2.  クライアント ドライバーのアイドル状態の IRP の完了 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) の状態\_POWER\_状態\_いずれかが保留中の場合は無効です。

一般的な親ドライバーは、次の条件のいずれかが true の場合、デバイスの USB ポートを中断します。

-   システムは低電力状態に遷移中です。
-   クライアント ドライバーの複合デバイス上のすべての関数を選択的に開始した中断します。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  



