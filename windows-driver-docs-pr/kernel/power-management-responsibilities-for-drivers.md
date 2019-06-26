---
title: ドライバーの電源管理の役割
description: ドライバーの電源管理の役割
ms.assetid: c42a5b95-76f3-4975-b452-4858bbbe532e
keywords:
- 電源管理の WDK カーネル、ドライバーの責任
- ドライバー power 責任 WDk カーネル
- WDK カーネルの電源を節約します。
- 電源管理の WDK カーネルの電源を状態します。
- 電源の状態の WDK カーネル
- WDK の電源管理を状態します。
- システム電源の状態の WDK カーネル、電源管理
- デバイスの電源状態の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c97fe28aec37109a93bf68e5d98c79cefd44074
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374197"
---
# <a name="power-management-responsibilities-for-drivers"></a>ドライバーの電源管理の役割





電源管理をサポートするドライバーは、責任を負います。

[デバイスの電源機能レポート](reporting-device-power-capabilities.md)PnP 列挙中にします。

[電源管理のデバイス オブジェクトのフラグを設定](setting-device-object-flags-for-power-management.md)します。

[電源 Irp の処理](handling-power-irps.md)電源マネージャーまたはドライバーによって送信されました。

[デバイスの電源を投入](powering-up-a-device.md)システムの起動時またはアイドル シャット ダウン後に必要なだけです。

[デバイスの電源](powering-down-a-device.md)システム シャット ダウン時刻または配置するときにスリープ状態にまで下がります。

[デバイスのウェイク アップを有効にする](enabling-device-wake-up.md)デバイスは、ウェイク アップ機能をサポートしている場合、します。

[デバイスのパフォーマンスの状態を管理する](managing-device-performance-states.md)場合、デバイスは減少のパフォーマンスをサポートしている電力消費量を減らす機能します。

すべてのデバイス スタックのすべてのドライバーは、これらすべてのタスクを実行します。 通常、バス ドライバーの機能の報告、フラグを設定および物理デバイスを操作し、デバイスの電源ポリシー マネージャー (関数ドライバーでは、通常は) は、スリープ状態にウェイク アップを有効にして、デバイスへの要求を発行します。

いくつかの例外を除き、ドライバーの電源投入および自分のデバイスをオフ、電源 Irp、大規模なコードでは、Irp への応答でウェイク アップのデバイスを有効にする、 [ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power). Irp の電源は、ドライバーによって電源マネージャーによって、場合によっては、送信できます。

 

 




