---
title: PoStartNextPowerIrp の呼び出し
description: PoStartNextPowerIrp の呼び出し
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- Irp WDK カーネル、PoStartNextPowerIrp を電源します。
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f1e9f36d60ede49f55579bc8eab1224e647bae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385261"
---
# <a name="calling-postartnextpowerirp"></a>PoStartNextPowerIrp の呼び出し





Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、クエリ性能 IRP またはセット power IRP では、ドライバーが処理された後、ドライバー呼び出す必要があります**PoStartNextPowerIrp**電源マネージャー別に受信する準備ができたことを通知するにはIRP の電源を入れます。 ドライバーを呼び出す必要があります**PoStartNextPowerIrp** IRP の中にスタックを現在のドライバーを呼び出す前に、ロケーション ポイント[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)します。

ドライバーは各このルーチンを 1 回呼び出す必要があります[ **IRP\_MN\_クエリ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)または[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)受信した要求。 ドライバーを呼び出す必要はありません**PoStartNextPowerIrp**処理するときに[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)または[**IRP\_MN\_POWER\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)要求。

ドライバーを呼び出すと**PoStartNextPowerIrp**、IRP スタックの現在の場所は、現在のドライバーを指す必要があります。 一般的な規則としてこの最適から呼び出し、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。 **PoStartNextPowerIrp**する前に呼び出す必要があります[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)、 [ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、**PoCallDriver**します。 その他の順序で、ルーチンを呼び出すと、システム デッドロックが発生する可能性があります。

呼び出す必要がありますそれにもかかわらず、ドライバーが IRP が失敗した場合でも**PoStartNextPowerIrp**電源マネージャー別 power IRP を処理する準備ができたことを通知するためにします。

次のセクションを明確にはドライバーの種類ごとにこのルーチンを呼び出す必要があります。

[フィルター ドライバーから呼び出す PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[デバイスの電源ポリシー所有者から PoStartNextPowerIrp の呼び出し](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[PoStartNextPowerIrp を呼び出す、バス ドライバーから](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




