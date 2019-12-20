---
title: UMDF での電源ポリシーの所有権
description: UMDF での電源ポリシーの所有権
ms.assetid: cf543259-3401-4f3b-a492-53940cea07f3
keywords:
- 電源ポリシーの所有権 WDK UMDF
- 電源ポリシーの所有権 WDK UMDF、概要
- 電源管理 WDK UMDF、電源ポリシーの所有権
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d840ba35d04a148a9ad18dda887615d500f8fb
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210908"
---
# <a name="power-policy-ownership-in-umdf"></a>UMDF での電源ポリシーの所有権


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

デバイスごとに、デバイスのドライバーの1つ (1 つだけ) がデバイスの*電源ポリシーの所有者*である必要があります。 電源ポリシーの所有者は、デバイスの適切な[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)を判断し、デバイスの電源状態が変更されるたびにデバイスのドライバースタックに要求を送信します。

フレームワークベースのドライバーには、デバイスの電源状態の変更を要求するコードが含まれていません。これは、フレームワークによってそのコードが提供されるためです。 既定では、システムが[スリープ状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-sleeping-states)になるたびに、フレームワークはデバイスのバスのドライバーに対してデバイスの電力状態を D3 に下げるように要求します。 (デバイスがウェイクアップ機能を提供している場合、デバイスのスリープ状態が D1 または D2 に設定されるように、ドライバーによって既定の動作が変更される可能性があります)。システムの電源が[正常な状態 (S0)](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-working-state-s0)に戻ると、フレームワークは、デバイスを動作 (D0) 状態に復元するようにバスドライバーに要求します。

電源ポリシーの所有者は、次のデバイス機能を有効または無効にする役割も担います。

-   デバイスがアイドル状態で、システムが動作中 (S0) 状態のままになっている場合に、デバイスが[低電力 (スリープ状態) 状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)に入る機能

-   外部イベントを検出したときにスリープ状態からスリープ解除するデバイスの機能

-   外部イベントを検出したときにシステムのスリープ状態からシステム全体をウェイクアップするデバイスの能力

デバイスでこれらのアイドル状態の電源とシステムのウェイクアップ機能がサポートされている場合、電源ポリシーの所有者は、一連の電源ポリシーイベントコールバック関数を定義するフレームワークの[IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)インターフェイスと[IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)インターフェイスをサポートすることもできます。

既定では、UMDF ベースのドライバーは電源ポリシーの所有者ではありません。 デバイスのカーネルモード関数ドライバーは、既定の電源ポリシーの所有者です。 (カーネルモードの関数ドライバーがなく、バスドライバーが[**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)を呼び出している場合、バスドライバーは電源ポリシーの所有者です)。 UMDF ベースのドライバーをドライバースタックの電源ポリシーの所有者にする場合、ドライバーは[**Iwdfdeviceinitialize:: SetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setpowerpolicyownership)を呼び出す必要があります。また、カーネルモードの既定の電源ポリシー所有者は、 [**Wdfdeviceinitsetpowerpolicyオーナーシップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)を呼び出して所有権を無効にする必要があります。

さらに、USB デバイス用に UMDF ベースのドライバーを提供していて、ドライバーを電源ポリシーの所有者にする場合は、ドライバーの INF ファイルに、レジストリの WinUsbPowerPolicyOwnershipDisabled 値を設定する[**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)が含まれている必要があります。 この REG\_DWORD サイズの値が0以外の数値に設定されている場合は、デバイスの電源ポリシーの所有者である[Winusb](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)ドライバーの機能が無効になります。 次の例に示すように、AddReg ディレクティブは、 [**INF DDInstall. HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)に存在する必要があります。

```cpp
[MyDriver_Install.NT.hw]
AddReg=MyDriver_AddReg

[MyDriver_AddReg]
HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
```

このフレームワークは、電源ポリシーの所有者に対して次の作業を行います。

-   ドライバーとその他のドライバースタック間のすべての電源ポリシー通信を処理します。 たとえば、フレームワークによって要求が行われるため、ドライバーはデバイスの電源状態を変更するようにバスドライバーに要求する必要はありません。

-   ドライバーが電源ポリシーイベントコールバック関数を登録している場合、デバイスが低電力状態からスリープ解除できるようにする時間が経過すると、フレームワークはそれらを呼び出します。

-   ユーザーがドライバーでアイドル設定とウェイク設定を変更できるようにすると、フレームワークによって、デバイスマネージャー表示されるプロパティシートページの形式でユーザーインターフェイスが提供されます。

電源ポリシー所有者の責任の詳細については、次のトピックを参照してください。

-   [UMDF ベースのドライバーでのアイドル状態の電源をサポートする](supporting-idle-power-down-in-umdf-drivers.md)

-   [UMDF ベースのドライバーでのシステムウェイクアップのサポート](supporting-system-wake-up-in-umdf-drivers.md)

-   [UMDF でのデバイスのアイドル状態とウェイク動作のユーザーコントロール](user-control-of-device-idle-and-wake-behavior-in-umdf.md)

 

 





