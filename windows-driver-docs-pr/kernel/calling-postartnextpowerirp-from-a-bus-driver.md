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
ms.openlocfilehash: 337eb2b92772d5da8513dce6a16c4e14afff047d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338611"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>バス ドライバーからの PoStartNextPowerIrp の呼び出し





Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、バス ドライバーを呼び出す必要があります**PoStartNextPowerIrp**に対して 1 回ごと[ **IRP\_MN\_クエリ\_電源** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)または[ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)ドライバーが受信した要求。

常に、バス ドライバーにこのルーチンを呼び出すその*DispatchPower*ルーチンを呼び出す前に、 [ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)ルーチン。

 

 




