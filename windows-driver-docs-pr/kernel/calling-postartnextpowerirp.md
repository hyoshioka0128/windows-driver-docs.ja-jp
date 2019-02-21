---
title: PoStartNextPowerIrp を呼び出す
description: PoStartNextPowerIrp を呼び出す
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- Irp WDK カーネル、PoStartNextPowerIrp を電源します。
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa55bfc81e8c8ebf9182c8a527c1e4ecacb305c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552084"
---
# <a name="calling-postartnextpowerirp"></a>PoStartNextPowerIrp を呼び出す





Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、クエリ性能 IRP またはセット power IRP では、ドライバーが処理された後、ドライバー呼び出す必要があります**PoStartNextPowerIrp**電源マネージャー別に受信する準備ができたことを通知するにはIRP の電源を入れます。 ドライバーを呼び出す必要があります**PoStartNextPowerIrp** IRP の中にスタックを現在のドライバーを呼び出す前に、ロケーション ポイント[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)します。

ドライバーは各このルーチンを 1 回呼び出す必要があります[ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)または[ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)受信した要求。 ドライバーを呼び出す必要はありません**PoStartNextPowerIrp**処理するときに[ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)または[**IRP\_MN\_POWER\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/ff551644)要求。

ドライバーを呼び出すと**PoStartNextPowerIrp**、IRP スタックの現在の場所は、現在のドライバーを指す必要があります。 一般的な規則としてこの最適から呼び出し、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。 **PoStartNextPowerIrp**する前に呼び出す必要があります[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、 [ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)、**PoCallDriver**します。 その他の順序で、ルーチンを呼び出すと、システム デッドロックが発生する可能性があります。

呼び出す必要がありますそれにもかかわらず、ドライバーが IRP が失敗した場合でも**PoStartNextPowerIrp**電源マネージャー別 power IRP を処理する準備ができたことを通知するためにします。

次のセクションを明確にはドライバーの種類ごとにこのルーチンを呼び出す必要があります。

[フィルター ドライバーから呼び出す PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[デバイスの電源ポリシー所有者から PoStartNextPowerIrp の呼び出し](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[PoStartNextPowerIrp を呼び出す、バス ドライバーから](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




