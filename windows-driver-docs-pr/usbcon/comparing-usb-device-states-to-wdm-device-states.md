---
Description: このトピックでは、ユニバーサルシリアルバス2.0 仕様のセクション9.1 で指定されているように、USB デバイスの電源状態に使用する WDM デバイスの状態について説明します。
title: USB デバイスの電源状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed683b2d7c451059d0554c8da79514298202af30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842403"
---
# <a name="usb-device-power-states"></a>USB デバイスの電源状態


このトピックでは、ユニバーサルシリアルバス2.0 仕様のセクション9.1 で指定されているように、USB デバイスの電源状態に使用する WDM デバイスの状態について説明します。

USB デバイスの電源状態 (Universal Serial Bus 2.0 仕様のセクション9.1 で規定) は、次の3つの一般的なカテゴリに分類できます。

-   [アタッチ済み]: デバイスは接続されていますが、完全には電源が入っていません。
-   電源: デバイスは、完全な状態 (既定、アドレス、または構成済み) のいずれかになっています。
-   [中断]: デバイスはアイドル状態で、低電力で動作しています。

WDM 電源モデルに定義されているデバイスの電源状態と USB 標準で定義されているデバイスの電源の状態の間に直接的な相関関係はありません。 たとえば、"*一時停止*" と "*アイドル*" という用語は、USB 仕様で非常に具体的な意味を持ちます。ただし、これらの用語は多くの場合、WDM 電源モデルでは異なる方法で使用されます。 Windows クライアントドライバーは、USB デバイスを中断状態にすることができます。 詳細については、「 [USB 選択的中断](usb-selective-suspend.md)」を参照してください。 クライアントドライバーは、デバイスを中断する準備が整うと、バスドライバーに対してアイドル状態を指示します。 アイドル状態の要求の詳細については、「 [USB 選択的中断](usb-selective-suspend.md)」を参照してください。

WDM モデルのデバイスの電源状態は、次のようにまとめることができます。

-   **D0** -動作状態。 デバイスの電源が完全に切れている。
-   **D1/D2** -中間スリープ状態。 これらの状態により、デバイスでリモートウェイクアップを行うことができます。
-   **D3** -最も深いスリープ状態です。 状態が**D3**のデバイスは、リモートでウェイクアップできません。

WDM 電源モデルのデバイスの電源状態の詳細については、「[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)」を参照してください。

WDM 電源モデルは、リモートウェイクアップ用のデバイスの*取り組ま*という用語を使用します。 取り組まは、通常はそうではないソフトウェア操作であり、USB デバイスでリモートウェイクアップ機能を*有効*にするハードウェア操作につながります。 リモートウェイクアップのためにデバイスをアームする WDM ソフトウェア操作は、待機ウェイク IRP ([**irp\_\_wait\_wake**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) です。 この IRP の詳細については、「[ウェイクアップ機能を搭載したデバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)」を参照してください。

このソフトウェア操作と USB リモートウェイクアップ機能の有効化の関係の詳細については、「[リモートウェイクアップ (Usb デバイスの](remote-wakeup-of-usb-devices.md))」を参照してください。

ここでは、次のサブセクションについて説明します。

-   [非複合デバイスの電源状態の変更](#changing-the-power-state-of-a-non-composite-device)
-   [複合デバイスの電源状態の変更](#changing-the-power-state-of-a-composite-device)
-   [関連トピック](#related-topics)

## <a name="changing-the-power-state-of-a-non-composite-device"></a>非複合デバイスの電源状態の変更


USB デバイスの電源ポリシーマネージャーは、デバイスの電源状態を設定する役割を担います。 電源ポリシーマネージャーは、WDM 電源 ([**irp\_\_SET\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) IRP を発行して電源状態を設定します。 電源ポリシーマネージャーの詳細については、「[電源ポリシーの所有権](https://docs.microsoft.com/windows-hardware/drivers/wdf/power-policy-ownership)」を参照してください。

バスドライバーによって実行される操作は、電源ポリシーマネージャーが要求するデバイスの電源レベルによって異なります。 次に、バスドライバーが各レベルの電源要求の実行に対して行うアクションを示します。

-   **D0**

    バスドライバーは、次のタスクを実行します。

    1.  すべての upsteam USB ハブの電源が入っており、要求を受信する準備ができていることを確認します。
    2.  デバイスの USB ポートが中断されている場合は、ポート\_SUSPEND 機能をオフにして、ポートを再開します。
    3.  デバイスのアイドル状態が保留中の場合は、状態\_SUCCESS で完了します。
    4.  リモートウェイクアップ用にデバイスを無効にします (これが行われた場合)。
-   **D1/D2**

    バスドライバーは、次のタスクを実行します。

    1.  待機ウェイク IRP ([**IRP\_\_wait\_wake**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) が保留中の場合、リモートウェイクアップのためにデバイスをアームします。
    2.  ポート\_SUSPEND 機能を設定して、デバイスの USB ポートを中断します。
-   **D3**

    バスドライバーは、次のタスクを実行します。

    1.  ポート\_SUSPEND 機能を設定して、デバイスの USB ポートを中断します。
    2.  デバイスの wait wake IRP を、状態\_電源\_状態で完了します (保留中の場合)\_無効です。
    3.  デバイスのアイドル状態の IRP[ **\_(内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を完了します。状態が保留中の場合は、電源\_状態\_無効になります。\_

## <a name="changing-the-power-state-of-a-composite-device"></a>複合デバイスの電源状態の変更


複合デバイス上のインターフェイスのクライアントドライバーは、複合デバイスの電源状態と、デバイス上の他のインターフェイスのクライアントドライバーを共有する必要があります。 そのため、インターフェイスのクライアントドライバーは、デバイス上の他のインターフェイスに影響を与えずに、複合デバイスを低電力状態にすることはできません。 [USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)は、インターフェイスのクライアントドライバーが、[**電源要求\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_送信するときに、次の操作を実行します。

-   **D0**

    バスドライバーは、次のタスクを実行します。

    1.  すべての upsteam USB ハブの電源が入っており、要求を受信する準備ができていることを確認します。
    2.  デバイスの USB ポートが中断されている場合は、ポート\_SUSPEND 機能をオフにして、ポートを再開します。
    3.  クライアントドライバーのアイドル状態の IRP を完了します (状態が保留中の場合)。\_成功した場合はを返します。
-   **D1/D2**

    バスドライバーは操作を実行しません。

-   **D3**

    バスドライバーは、次のタスクを実行します。

    1.  クライアントドライバーの wait wake IRP (IRP\_\_WAIT\_WAKE\_) を完了します。電源\_状態は、保留中の場合は無効\_無効になります。
    2.  クライアントドライバーのアイドル状態の IRP[ **\_(内部\_USB\_送信\_アイドル\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) を完了します。状態が保留中の場合は、電源\_状態\_無効になります。\_

次のいずれかの条件に該当する場合、汎用の親ドライバーはデバイスの USB ポートを中断します。

-   システムが低電力状態に移行しています。
-   複合デバイス上のすべての関数のクライアントドライバーが、選択的中断を開始しました。

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  



