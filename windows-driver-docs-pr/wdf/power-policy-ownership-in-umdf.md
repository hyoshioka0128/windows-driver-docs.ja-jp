---
title: UMDF で電源ポリシーの所有権
description: UMDF で電源ポリシーの所有権
ms.assetid: cf543259-3401-4f3b-a492-53940cea07f3
keywords:
- 電源ポリシー所有権 WDK UMDF
- 電源ポリシー所有権 WDK UMDF, 概要
- 電源管理 WDK UMDF、電源ポリシーの所有権
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c84a595b0e187b6a372b4e5df99d33970b70b191
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552270"
---
# <a name="power-policy-ownership-in-umdf"></a>UMDF で電源ポリシーの所有権


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

各デバイス、いずれか (および 1 つだけ)、デバイスのドライバーのデバイスをする必要があります*電源ポリシー所有者*します。 電源ポリシー所有者は、適切な決定[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)デバイスの電源の状態が変更されるたびに、デバイスのドライバー スタックへのデバイスと送信要求。

フレームワーク ベースのドライバーが要求するコードを含まない、フレームワークがそのコードを提供するため、デバイスの電力状態に変更します。 既定では、ときに、システムが入力、[システムがスリープ状態](https://msdn.microsoft.com/library/windows/hardware/ff564575)フレームワークは D3 にデバイスの電源状態を削減するデバイスのバスのドライバーを確認します。 (、ドライバーように変更できます既定の動作、フレームワーク、D1 または D2 にデバイスのスリープ状態を設定する場合は、デバイスは、ウェイク アップ機能を提供します。)システムの電源が返されるときにその[(S0) の状態を操作](https://msdn.microsoft.com/library/windows/hardware/ff564591)フレームワークの作業 (D0) 状態にデバイスを復元するバス ドライバーを要求します。

電源ポリシー所有者は有効にして、次のデバイス機能を無効にする責任を負いますもです。

-   入力する、デバイスの機能、 [(スリープ) 低電力状態](https://msdn.microsoft.com/library/windows/hardware/ff543186)がアイドル状態とシステムの作業 (S0) 状態のままになります

-   外部イベントが検出されたときに、スリープ状態から復帰自体、デバイスの機能

-   システム全体のシステムの外部イベントを検出した場合に、スリープ状態から復帰するデバイスの機能

デバイスは、これらのアイドル状態の電源とシステムのウェイク アップ機能をサポートする場合、電源ポリシー所有者フレームワークにもサポートできます[IPowerPolicyCallbackWakeFromS0](https://msdn.microsoft.com/library/windows/hardware/ff556815)と[IPowerPolicyCallbackWakeFromSx](https://msdn.microsoft.com/library/windows/hardware/ff556825)インターフェイスで、電源ポリシー イベントのコールバック関数のセットを定義します。

既定では、UMDF ベースのドライバーと、電源ポリシーの所有者ではありません。 デバイスのカーネル モードの機能のドライバーは、既定の電源ポリシー所有者です。 (カーネル モードの関数のドライバーがないと、バス ドライバーと呼ばれる場合[ **WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)、バス ドライバーは、電源ポリシー所有者)。 ドライバーを呼び出す必要があります、UMDF に基づくドライバーをドライバー スタックの電源ポリシー所有者である場合は、 [ **IWDFDeviceInitialize::SetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff557001)、およびカーネル モードの既定の電源ポリシー所有者が呼び出す必要があります[ **WdfDeviceInitSetPowerPolicyOwnership** ](https://msdn.microsoft.com/library/windows/hardware/ff546776)所有権を無効にします。

また、USB デバイスの UMDF ドライバーを指定して、ドライバーは、電源ポリシーの所有者である場合は、ドライバーの INF ファイルを含める必要があります、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)設定、レジストリの WinUsbPowerPolicyOwnershipDisabled 値。 場合この REG\_DWORD のサイズの値が 0 以外の任意の数に設定を無効になります、 [WinUSB](https://msdn.microsoft.com/library/windows/hardware/ff540196)ドライバーの機能、デバイスの電源ポリシー所有者にします。 AddReg ディレクティブがである必要があります、 [ **INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)、次の例を示しています。

```cpp
[MyDriver_Install.NT.hw]
AddReg=MyDriver_AddReg

[MyDriver_AddReg]
HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
```

フレームワークは、次の作業を電源ポリシー所有者には。

-   ドライバーとドライバー スタックの残りの部分の間のすべての電源ポリシー通信を処理します。 など、ドライバーはフレームワークは、要求を行うために、デバイスの電源の状態を変更するバス ドライバーを要求する必要はありません。

-   ドライバーは、電源ポリシー イベントのコールバック関数を登録場合、フレームワークに時期を有効または低電力状態からスリープ状態を解除するデバイスの機能を無効になったときにします。

-   ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、デバイス マネージャーを表示するプロパティ シート ページの形式でユーザー インターフェイスを提供します。

電源ポリシー所有者の責任についての詳細については、次のトピックを参照してください。

-   [UMDF ベースのドライバーでのアイドル状態の電源のサポート](supporting-idle-power-down-in-umdf-drivers.md)

-   [UMDF ベースのドライバーでのシステムのウェイク アップのサポート](supporting-system-wake-up-in-umdf-drivers.md)

-   [デバイスのユーザーによる制御がアイドル状態し、復帰の UMDF での動作](user-control-of-device-idle-and-wake-behavior-in-umdf.md)

 

 





