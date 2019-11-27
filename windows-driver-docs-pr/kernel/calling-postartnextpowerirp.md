---
title: PoStartNextPowerIrp の呼び出し
description: PoStartNextPowerIrp の呼び出し
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- 電源 Irp WDK カーネル、PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01721a79c79fcb7f2d25a631722e2a5e0201b8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828580"
---
# <a name="calling-postartnextpowerirp"></a>PoStartNextPowerIrp の呼び出し





Windows Vista 以降では、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出す必要はなく、このルーチンを呼び出すと電源管理操作は実行されません。 ただし、Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーがクエリ-電源 IRP または set-power IRP を処理した後、ドライバーは**Postartnextpowerirp**を呼び出して、別の電源 irp を受信する準備ができたことを電源マネージャーに通知する必要があります。 IRP スタックの場所が現在のドライバーを指し、 [**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出す前に、ドライバーは**Postartnextpowerirp**を呼び出す必要があります。

ドライバーは、各[**IRP\_\_クエリ\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)または irp\_、受信した[ **\_電力要求\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されている場合に、このルーチンを一度呼び出す必要があります。 Irp\_を処理するときに、ドライバーは**Postartnextpowerirp**を呼び出す必要はありません。 [ **\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)または[**IRP\_、電力\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)要求を\_します。

ドライバーが**Postartnextpowerirp**を呼び出す場合、現在の IRP スタックの場所は現在のドライバーを指している必要があります。 一般的な規則として、この呼び出しは[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンから行うことをお勧めします。 **Postartnextpowerirp**は、IoCompleteRequest、 [**ioskip enti Stacklocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、 **pocalldriver**の前に呼び出す必要があります。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 他の順序でルーチンを呼び出すと、システムのデッドロックが発生する可能性があります。

ドライバーが IRP に障害を出した場合でも、他の電源 IRP を処理する準備ができていることをパワーマネージャーに通知するために、 **Postartnextpowerirp**を呼び出す必要があります。

次のセクションでは、各種類のドライバーがこのルーチンを呼び出すタイミングを明確にします。

[フィルタードライバーから PoStartNextPowerIrp を呼び出しています](calling-postartnextpowerirp-from-a-filter-driver.md)

[デバイスの電源ポリシー所有者から PoStartNextPowerIrp を呼び出しています](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[バスドライバーから PoStartNextPowerIrp を呼び出しています](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




