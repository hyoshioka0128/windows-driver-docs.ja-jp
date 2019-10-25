---
title: 電源ポリシーの所有権
description: 電源ポリシーの所有権
ms.assetid: 8e44eedd-6afe-45c6-bbe8-42cfb6f6a644
keywords:
- 電源管理 WDK KMDF、所有権
- 所有権 WDK KMDF
- 所有権 WDK KMDF、電源ポリシー
- 電源ポリシー WDK KMDF
- ウェイクアップ機能 WDK KMDF
- スリープ電源管理 WDK KMDF
- 低電力状態 WDK KMDF
- デバイスの電源状態 WDK KMDF
- 作業状態 WDK KMDF
- 電源状態 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1d1ae68c608648d512dd879d6f5983af947bb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842242"
---
# <a name="power-policy-ownership"></a>電源ポリシーの所有権


デバイスごとに、デバイスのドライバーの1つ (1 つだけ) がデバイスの*電源ポリシーの所有者*である必要があります。 電源ポリシーの所有者は、デバイスの適切な[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)を判断し、デバイスの電源状態が変更されるたびにデバイスのドライバースタックに要求を送信します。

フレームワークベースのドライバーには、デバイスの電源状態の変更を要求するコードが含まれていません。これは、フレームワークによってそのコードが提供されるためです。 既定では、システムが[スリープ状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)になるたびに、フレームワークはデバイスのバスのドライバーに対してデバイスの電力状態を D3 に下げるように要求します。 (デバイスがウェイクアップ機能を提供している場合、デバイスのスリープ状態が D1 または D2 に設定されるように、ドライバーによって既定の動作が変更される可能性があります)。システムの電源が[正常な状態 (S0)](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)に戻ると、フレームワークは、デバイスを動作 (D0) 状態に復元するようにバスドライバーに要求します。

電源ポリシーの所有者は、次のデバイス機能を有効または無効にする役割も担います。

-   デバイスがアイドル状態で、システムが動作中 (S0) 状態のままになっている場合に、デバイスが[低電力 (スリープ状態) 状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)に入る機能

-   外部イベントを検出したときにスリープ状態からスリープ解除するデバイスの機能

-   外部イベントを検出したときにシステムのスリープ状態からシステム全体をウェイクアップするデバイスの能力

デバイスでこれらのアイドル状態の電源とシステムのウェイクアップ機能がサポートされている場合、電源ポリシーの所有者は、 [**Wdfdeviceinitsetpowerpolicyeventcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)を呼び出して、一連の電源ポリシーイベントコールバック関数を登録することもできます。

既定では、フレームワークベースのドライバーの場合、デバイスの関数ドライバーは電源ポリシーの所有者になります。 (関数ドライバーがなく、バスドライバーが[**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)を呼び出している場合、バスドライバーは電源ポリシーの所有者です)。 ドライバースタックの電源ポリシーの所有者を変更する場合は、既定の電源ポリシーの所有者が[**Wdfdeviceinitsetpowerpolicyownership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)を呼び出して所有権を無効にする必要があります。また、電源ポリシーの所有者は、を呼び出す**必要があります。** の所有権を有効にするには、WdfDeviceInitSetPowerPolicyOwnership を使用します。

このフレームワークは、電源ポリシーの所有者に対して次の作業を行います。

-   ドライバーとその他のドライバースタック間のすべての電源ポリシー通信を処理します。 たとえば、フレームワークによって要求が行われるため、ドライバーはデバイスの電源状態を変更するようにバスドライバーに要求する必要はありません。

-   ドライバーが電源ポリシーイベントコールバック関数を登録している場合、デバイスが低電力状態からスリープ解除できるようにする時間が経過すると、フレームワークはそれらを呼び出します。

-   ユーザーがドライバーでアイドル設定とウェイク設定を変更できるようにすると、フレームワークによって、デバイスマネージャー表示されるプロパティシートページの形式でユーザーインターフェイスが提供されます。

電源ポリシー所有者の責任の詳細については、次のトピックを参照してください。

-   [アイドル状態の電源をサポートする](supporting-idle-power-down.md)
-   [システムウェイクアップのサポート](supporting-system-wake-up.md)
-   [デバイスのアイドル状態とウェイク動作のユーザーコントロール](user-control-of-device-idle-and-wake-behavior.md)
-   [機能力状態のサポート](supporting-functional-power-states.md)

 

 





