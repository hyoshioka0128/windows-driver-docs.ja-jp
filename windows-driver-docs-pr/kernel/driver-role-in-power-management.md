---
title: 電源管理でのドライバーの役割
description: 電源管理でのドライバーの役割
ms.assetid: 24b55880-e767-4f18-977e-c4a93332b909
keywords:
- 電源管理の WDK カーネル、ドライバーのロール
- システム電源の状態 WDK カーネル、ドライバーの役割
- デバイスの電源状態の WDK カーネル
- ドライバーの電源のサポートの役割 WDk カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a8f19f06ebaf779ba8015659ebe27e65ec71d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353001"
---
# <a name="driver-role-in-power-management"></a>電源管理でのドライバーの役割





ドライバーは、2 つの方法で電源管理をサポートします。

1.  ドライバーは、電源マネージャーから発行されたシステムの電源の要求に応答します。

2.  ドライバーの管理能力とパフォーマンスの個々 のデバイスの状態。

すべてのドライバーが必要、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)を処理するルーチン[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求。 *DispatchPower*ルーチンは、各 power IRP を調べる必要があるし、それを処理するかまたは次の下位ドライバーに渡します。

電源管理に参加するデバイスの場合、デバイスのデバイス スタックのすべてのドライバーに応答したり、power Irp を適切に渡す必要があります。 1 つのドライバーの障害を正しく動作するには、電源管理をシステム全体で無効にすることがあります。

デバイスごとに 1 つのドライバー[電源ポリシーの管理](managing-device-power-policy.md)そのデバイス用です。 そのドライバーは、そのデバイスの電源操作を実行するには、独自デバイス スタックを power Irp を送信できます。 電源ポリシー マネージャーは、システム電源の Irp にデバイスの電源を対応する Irp を発行します。

さらに、ドライバーが起動時にデバイスの電源を入れてまたは電源 IRP を受信せずに削除すると、デバイスを切るなど、特定の電源のタスクを実行する可能性があります。 これらは、暗黙的な電源要求と見なされます。

詳細については、次を参照してください。[ドライバーの電源管理の責任](power-management-responsibilities-for-drivers.md)します。

 

 




