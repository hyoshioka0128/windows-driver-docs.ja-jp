---
title: フィルター ドライバーでのシステム電源設定 IRP の処理
description: フィルター ドライバーでのシステム電源設定 IRP の処理
ms.assetid: a6e364fc-f173-47ce-b36b-84f802cefcc3
keywords:
- セット power Irp WDK の電源管理
- フィルター ドライバー WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 896993bd5712411a84b734e1057825625dc45c60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384245"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>フィルター ドライバーでのシステム電源設定 IRP の処理





すべてのフィルター ドライバーとそのデバイス スタックの電源ポリシーを所有していない任意の関数のドライバーでは、システムを渡す必要がありますだけに、次の手順で、次の下位ドライバー セット power IRP:

1.  呼び出す[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を完了して、エラー状態を返すにします。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは呼び出す必要がありますまず[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)、呼び出す**IoCompleteRequest** IRP の完了にし、エラー状態を返します。

2.  呼び出す**PoStartNextPowerIrp** IRP の [次へ] のパワーを開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

3.  IRP スタックの場所の設定 ([**IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)または[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext))。 ドライバーを設定できる、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP がそうでルーチンは必要なことはほとんどありません。

4.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (で Windows 7 および Windows Vista の場合) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、Windows 2000 で)次の下位ドライバーには、IRP を渡す。

5.  呼び出す[ **IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)します。 ただし、ドライバーを設定する場合、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、IRP のルーチンからには、この呼び出しを行う、 *IoCompletion*ルーチン代わりにします。

6.  状態を返す\_PENDING からその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




