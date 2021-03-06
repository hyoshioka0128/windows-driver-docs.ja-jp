---
title: 待機/ウェイク操作の概要
description: 待機/ウェイク操作の概要
ms.assetid: 63453f7e-f656-4efc-bb44-9e2cb0232270
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- 待機/ウェイク Irp の待機またはスリープ解除についての Irp WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1acc028863d6c9652d73490da8c73b1f61385b7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383829"
---
# <a name="overview-of-waitwake-operation"></a>待機/ウェイク操作の概要





次の図に示すように、オペレーティング システムのウェイク アップのメカニズムの動作します。

![irp の概要を示す図\-mn\-待機\-wake 処理](images/send-waitwake.png)

1.  システムとデバイスは、作業の状態では、デバイスの電源ポリシー所有者は、(「取得」) のウェイク アップのデバイスを有効にする必要がありますを決定します。 電源ポリシー所有者 power IRP の要求 ([**PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)でコードを少し[ **IRP\_MN\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake))、デバイス スタックのすべてのドライバーを通知するために、PDO に送信します。 ポリシー所有者を要求内には、コールバック ルーチンを指定します (とは異なります、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン)。

2.  I/O マネージャーを通じて、電源マネージャーは、デバイス スタックの先頭に IRP を送信します。

3.  ドライバー セット*IoCompletion*までダウン IRP がバス ドライバーに達するとルーチンを渡します。

4.  バス ドライバーは、物理デバイスでウェイク アップをできるようにして、保留中の IRP をマークする場合。 必要に応じて、また、その親の待機/ウェイク IRP を要求します。

5.  その後、外部からウェイク アップの信号が到着します。

6.  バス ドライバーが完了すると、 **IRP\_MN\_待機\_WAKE**します。

7.  I/O マネージャー呼び出し*IoCompletion*ドライバーは IRP を渡すように設定されたルーチンがスタックをダウンします。

8.  I/O マネージャーは、IRP を要求したときに、ポリシーの所有者によって設定するコールバック ルーチンを呼び出します。

**IRP\_MN\_待機\_WAKE**要求では、デバイスまたはシステムの電源の状態は変更されません。 デバイスのウェイク アップだけで有効、後で場合は、デバイスが適切なスリープ状態になる、外部からの信号と、デバイス (と可能性があるシステム) がスリープ解除するようにします。

ウェイク アップの信号が到着すると、ドライバーの動作は、同じシステムまたは自体のみ、デバイスがアクティブかどうか。 ウェイク アップのデバイスが有効になっているし、システムが元となる、デバイスがスリープ解除がスリープ状態では場合、デバイスは、システムがスリープ解除します。 ウェイク アップのデバイスが有効になっているし、システムが稼働状態場合、デバイスのみを再開します。

コンピューターとデバイスが異なるため、設計の 電源平面、特にに関して、サポートされているシステムとデバイスの電源状態の--外となります待機/ウェイク--をサポートできる状態すべてのハードウェア構成で同じです。 そのため、そのデバイスの電源ポリシーを所有している任意のドライバーとすべてのバス ドライバーが実行されている個々 の構成の機能に注意を払う必要があります。 詳細については、次を参照してください。[デバイスが、システムのスリープを解除できるかどうかを決定する](determining-whether-a-device-can-wake-the-system.md)します。

待機またはスリープ解除操作の詳細については、次を参照してください。[デバイス ツリーを通じて待機/ウェイク Irp のパスを理解する](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)と[待機/ウェイク IRP の完了の概要](overview-of-wait-wake-irp-completion.md)します。

 

 




