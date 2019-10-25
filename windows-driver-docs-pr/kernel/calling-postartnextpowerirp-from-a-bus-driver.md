---
title: バス ドライバーからの PoStartNextPowerIrp の呼び出し
description: バス ドライバーからの PoStartNextPowerIrp の呼び出し
ms.assetid: 4e23ebe1-c939-48e1-82bf-cdb4980a5a7b
keywords:
- バスドライバーの WDK 電源管理
- 電源 Irp WDK カーネル、PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ae5fd43ab86c566d6cda8dbdf7c97aeb19e412
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837164"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>バス ドライバーからの PoStartNextPowerIrp の呼び出し





Windows Vista 以降では、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出す必要はなく、このルーチンの呼び出しによって電源管理操作は実行されません。 ただし、Windows Server 2003、Windows XP、および Windows 2000 では、バスドライバーは、すべての IRP [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) [ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)に対して**postartnextpowerirp**を1回呼び出す必要があります。ドライバーはを受信します。

バスドライバーは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)ルーチンを呼び出す前に、常に*DispatchPower*ルーチンでこのルーチンを呼び出します。

 

 




