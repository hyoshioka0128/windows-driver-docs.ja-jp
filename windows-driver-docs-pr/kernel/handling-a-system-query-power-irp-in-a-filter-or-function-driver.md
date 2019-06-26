---
title: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理
description: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理
ms.assetid: 81d921d5-6db8-4858-b86e-1484781faba5
keywords:
- クエリ power Irp WDK の電源管理
- フィルター ドライバー WDK の電源管理
- 関数のドライバー WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d979478552bcaff34c547670c2095049214657eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387008"
---
# <a name="handling-a-system-query-power-irp-in-a-filter-or-function-driver"></a>フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の処理





(これは、デバイスの電源ポリシー所有者ではありません)、フィルターまたは関数のドライバーがシステムに渡す必要があります、次の手順で、次の下位ドライバーにクエリ power IRP:

1.  呼び出す[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を完了して、エラー状態を返すにします。 ドライバーが呼び出すサーバーの Windows Server 2003、Windows XP、および Windows 2000、 [ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)、呼び出す**IoCompleteRequest** IRP の完了を返す、エラー状態です。

2.  クエリが失敗にするかどうかを決定します。 ガイドラインについては、次を参照してください。[フィルターまたは関数のドライバーで、システム クエリ性能の IRP を失敗](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)し、そのセクションで説明した処理を完了します。

3.  呼び出す[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)

4.  IRP スタックの場所の設定 ([**IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)または[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext))。 ドライバーを設定できる、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP がそうでルーチンは必要なことはほとんどありません。

5.  呼び出す**保留**(Windows 7、Windows Vista で) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、および Windows 2000) で、次の下位ドライバーに IRP を渡す。

6.  呼び出す[ **IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)します。 ただし、ドライバーを設定する場合、 *IoCompletion* 、IRP のルーチンからには、この呼び出しを行う、 *IoCompletion*ルーチン代わりにします。

7.  状態を返す\_PENDING からその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




