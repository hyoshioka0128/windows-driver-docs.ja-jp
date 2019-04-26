---
title: UMDF ドライバーでのシステム ウェイクアップのサポート
description: UMDF ドライバーでのシステム ウェイクアップのサポート
ms.assetid: 945b1751-f3a1-4a29-8fb7-6690f91af7d9
keywords:
- 電源管理 WDK UMDF、システムのウェイク アップ
- システム ウェイク アップ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a09dc7bd063a3132a65c68ce60dced5d2072d63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350736"
---
# <a name="supporting-system-wake-up-in-umdf-drivers"></a>UMDF ドライバーでのシステム ウェイクアップのサポート


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

システムは、低電力状態では、一部のデバイスは、受信ネットワーク パケットなどの外部イベントを検出し、システムのスリープ状態を解除できます。 たとえば、PCI デバイスがシステムのウェイク アップ機能では、デバイスの電源管理機能 (PMC) の登録に記載されているスリープ状態をシステム PCI バス上の電源管理イベント (PME) シグナルを発生させることで。

デバイスは、システム、システム全体の低電力状態からスリープ解除できる場合、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)でコールバック関数、[電源ポリシー所有者](power-policy-ownership-in-umdf.md)を実行する必要があります、次の 2 つの手順。

1.  呼び出す[ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)を指定します。
    -   デバイスが入力する低電力状態
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   デバイスのウェイク アップ機能を有効または無効にするかどうか

2.  実装、 [IPowerPolicyCallbackWakeFromSx](https://msdn.microsoft.com/library/windows/hardware/ff556825)インターフェイスと次イベント コールバック関数、デバイスの必要な場合。
    -   [**IPowerPolicyCallbackWakeFromSx::OnArmWakeFromSx**](https://msdn.microsoft.com/library/windows/hardware/ff556826)、ウェイク アップの外部イベントに応答するデバイスのハードウェアを有効にします。
    -   [**IPowerPolicyCallbackWakeFromSx::OnDisarmWakeFromSx**](https://msdn.microsoft.com/library/windows/hardware/ff556828)、ウェイク アップの外部イベントに応答するデバイスの機能を無効にします。
    -   [**IPowerPolicyCallbackWakeFromSx::OnWakeFromSxTriggered**](https://msdn.microsoft.com/library/windows/hardware/ff556833)バスがウェイク信号を検出、ドライバーに通知します。

バス ドライバーは、ウェイク アップするシステムにも参加します。 デバイスのバスのカーネル モード ドライバーでは、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

デバイスのウェイク アップ機能を制御するレジストリ エントリについては、次を参照してください。[ユーザー コントロールのデバイスがアイドル状態と UMDF Wake 動作](user-control-of-device-idle-and-wake-behavior-in-umdf.md)します。

 

 





