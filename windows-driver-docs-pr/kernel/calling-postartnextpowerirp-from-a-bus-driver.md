---
title: バス ドライバーからの PoStartNextPowerIrp の呼び出し
description: バス ドライバーからの PoStartNextPowerIrp の呼び出し
ms.assetid: 4e23ebe1-c939-48e1-82bf-cdb4980a5a7b
keywords:
- バス ドライバー WDK 電源管理
- Irp WDK カーネル、PoStartNextPowerIrp を電源します。
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5bce8e498f0ec7ee3f7acf8faa8c39c0d3c7a1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385270"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>バス ドライバーからの PoStartNextPowerIrp の呼び出し





Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、バス ドライバーを呼び出す必要があります**PoStartNextPowerIrp**に対して 1 回ごと[ **IRP\_MN\_クエリ\_電源** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)または[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)ドライバーが受信した要求。

常に、バス ドライバーにこのルーチンを呼び出すその*DispatchPower*ルーチンを呼び出す前に、 [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)ルーチン。

 

 




