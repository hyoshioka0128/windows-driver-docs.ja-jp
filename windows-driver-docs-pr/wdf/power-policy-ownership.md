---
title: 電源ポリシーの所有権
description: 電源ポリシーの所有権
ms.assetid: 8e44eedd-6afe-45c6-bbe8-42cfb6f6a644
keywords:
- 電源の WDK KMDF、所有権の管理
- WDK KMDF の所有権
- 所有権 WDK KMDF、電源ポリシー
- 電源ポリシー WDK KMDF
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- 低電力状態 WDK KMDF
- デバイスの電源状態が WDK KMDF
- 作業状態 WDK KMDF
- 電源状態が WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdfdddedab23c1b6e455b220804d10322e5ff36f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376346"
---
# <a name="power-policy-ownership"></a>電源ポリシーの所有権


各デバイス、いずれか (および 1 つだけ)、デバイスのドライバーのデバイスをする必要があります*電源ポリシー所有者*します。 電源ポリシー所有者は、適切な決定[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)デバイスの電源の状態が変更されるたびに、デバイスのドライバー スタックへのデバイスと送信要求。

フレームワーク ベースのドライバーが要求するコードを含まない、フレームワークがそのコードを提供するため、デバイスの電力状態に変更します。 既定では、ときに、システムが入力、[システムがスリープ状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)フレームワークは D3 にデバイスの電源状態を削減するデバイスのバスのドライバーを確認します。 (、ドライバーように変更できます既定の動作、フレームワーク、D1 または D2 にデバイスのスリープ状態を設定する場合は、デバイスは、ウェイク アップ機能を提供します。)システムの電源が返されるときにその[(S0) の状態を操作](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)フレームワークの作業 (D0) 状態にデバイスを復元するバス ドライバーを要求します。

電源ポリシー所有者は有効にして、次のデバイス機能を無効にする責任を負いますもです。

-   入力する、デバイスの機能、 [(スリープ) 低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)がアイドル状態とシステムの作業 (S0) 状態のままになります

-   夜間に起き出すそのものをスリープ状態から外部イベントを検出した場合に、デバイスの機能

-   システム全体のシステムの外部イベントを検出した場合に、スリープ状態から復帰するデバイスの機能

電源ポリシーの所有者を呼び出すことも、デバイスは、これらのアイドル状態の電源とシステムのウェイク アップ機能をサポートする場合[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)電源ポリシーのセットを登録するにはイベントのコールバック関数。

フレームワーク ベースのドライバーでは、既定では、デバイスの機能のドライバーは、電源ポリシー所有者です。 (関数ドライバーがないかどうかと、バス ドライバーが呼び出されて[ **WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)、バス ドライバーは、電源ポリシー所有者)。 ドライバー スタックの電源ポリシーの所有者を変更する場合は、既定の電源ポリシーの所有者を呼び出す必要があります[ **WdfDeviceInitSetPowerPolicyOwnership** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)所有権、およびとなるドライバーを無効にします電源ポリシーの所有者を呼び出す必要があります**WdfDeviceInitSetPowerPolicyOwnership**所有権を有効にします。

フレームワークは、次の作業を電源ポリシー所有者には。

-   ドライバーとドライバー スタックの残りの部分の間のすべての電源ポリシー通信を処理します。 など、ドライバーはフレームワークは、要求を行うために、デバイスの電源の状態を変更するバス ドライバーを要求する必要はありません。

-   ドライバーは、電源ポリシー イベントのコールバック関数を登録場合、フレームワークに時期を有効または低電力状態からスリープ状態を解除するデバイスの機能を無効になったときにします。

-   ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、デバイス マネージャーを表示するプロパティ シート ページの形式でユーザー インターフェイスを提供します。

電源ポリシー所有者の責任についての詳細については、次のトピックを参照してください。

-   [アイドル状態の電源のサポート](supporting-idle-power-down.md)
-   [システムのウェイク アップをサポートしています。](supporting-system-wake-up.md)
-   [デバイスがアイドル状態とスリープ解除の動作のユーザーによる制御](user-control-of-device-idle-and-wake-behavior.md)
-   [電源状態の機能をサポートしています。](supporting-functional-power-states.md)

 

 





