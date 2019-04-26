---
title: フィルター ドライバーでのシステム電源設定 IRP の処理
description: フィルター ドライバーでのシステム電源設定 IRP の処理
ms.assetid: a6e364fc-f173-47ce-b36b-84f802cefcc3
keywords:
- セット power Irp WDK の電源管理
- フィルター ドライバー WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09deaada5b6f5abf5a9fb86935524aa6d5e0e385
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359816"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>フィルター ドライバーでのシステム電源設定 IRP の処理





すべてのフィルター ドライバーとそのデバイス スタックの電源ポリシーを所有していない任意の関数のドライバーでは、システムを渡す必要がありますだけに、次の手順で、次の下位ドライバー セット power IRP:

1.  呼び出す[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP を完了して、エラー状態を返すにします。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは呼び出す必要がありますまず[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)、呼び出す**IoCompleteRequest** IRP の完了にし、エラー状態を返します。

2.  呼び出す**PoStartNextPowerIrp** IRP の [次へ] のパワーを開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

3.  IRP スタックの場所の設定 ([**IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)または[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387))。 ドライバーを設定できる、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP がそうでルーチンは必要なことはほとんどありません。

4.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (で Windows 7 および Windows Vista の場合) または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) (Windows Server 2003、Windows XP、Windows 2000 で)次の下位ドライバーには、IRP を渡す。

5.  呼び出す[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)します。 ただし、ドライバーを設定する場合、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、IRP のルーチンからには、この呼び出しを行う、 *IoCompletion*ルーチン代わりにします。

6.  状態を返す\_PENDING からその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




