---
title: デバイスの電源投入 IRP の処理
description: デバイスの電源投入 IRP の処理
ms.assetid: 8fcfd324-97f9-4fd0-8fa1-87685c6b5ec3
keywords:
- セット power Irp WDK カーネル
- デバイスが電源 Irp WDK カーネルを設定
- 電源 Irp WDK カーネル、デバイスの変更
- Irp WDK カーネルの電源投入
- スタートアップの電源管理の WDK カーネル
- WDK カーネルの電源を復元します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ce102ccbccf0a66ca817511b5038343086aa2b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386885"
---
# <a name="handling-device-power-up-irps"></a>デバイスの電源投入 IRP の処理





デバイスの電源投入 Irp 指定[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)とデバイスの電源状態を現在のデバイスの電源の状態より多くの電力を必要とします。 通常、パワーアップ IRP はデバイスの動作状態を指定します。 **PowerDeviceD0**します。

デバイスの電源を要求は、デバイスの場合、基になるバス ドライバーに、次に、スタック上に戻って連続する各ドライバー、最初に処理する必要があります。

次の図では、電源アップ IRP の処理に関連する手順を示します。

![デバイスの電源投入要求を処理するかを示す図](images/devd0.png)

処理するときに、 **IRP\_MN\_設定\_POWER**要求電源投入関数またはフィルター ドライバーにする必要があります。

-   呼び出す[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)ドライバーが受信しないことを確認する、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)パワーアップ IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を完了し、エラー状態を返します。 ドライバーが呼び出すサーバーの Windows Server 2003、Windows XP、および Windows 2000、 **IoCompleteRequest** IRP を完了するを呼び出すし[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)を開始する、IRP の電源を次に行い、エラー状態を返します。

-   呼び出す[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending) IRP の保留をマークします。

-   呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) IRP スタックの場所を設定します。 ドライバーを呼び出してはならない**IoSkipCurrentIrpStackLocation**が設定されている場合、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。

-   呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)電源投入を設定する*IoCompletion*ルーチン。

    ドライバーを設定する必要があります、デバイスの処理の電源投入 IRP、ときに、 *IoCompletion* IRP の完了後のタスクとデバイスの電源をルーチンにコンテキストを復元、削除ロックが解除、およびその他の実行が必要です。 IRP の完了前に、ドライバーはコンテキストを復元する必要があります。 詳細については、次を参照してください。[デバイス電源 Irp の IoCompletion ルーチン](iocompletion-routines-for-device-power-irps.md)します。

-   呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (で Windows 7 および Windows Vista の場合) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、および Windows 2000) する次の下位のドライバーに IRP を渡します。 IRP は、デバイス スタックの一番下バス ドライバーに移動する必要があります。 IRP の完了、バス ドライバーのみが許可されます。

-   状態を返す\_保留します。

デバイスがまだ存在を確認する必要があります最初、バス ドライバーは IRP を受信するとがされて削除されるかスリープ状態に置き換えられます。 デバイスは存在しない場合、バス ドライバーを呼び出す必要があります[ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)デバイスが消えたプラグ アンド プレイのマネージャーに通知する親デバイス。 このような状況で、デバイスがこのバス ドライバーに失敗することが IRP をパワーアップします。

バス ドライバーが呼び出しの操作状態をデバイスを返すために必要なタスクを実行しますし、デバイスがまだ存在する場合は、 [ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)新しいデバイスの電源の電源マネージャーに通知するには状態、および IRP の完了 ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest))。 ドライバーが、デバイスがスリープ状態の間に I/O がキューにまたは、デバイスに突入パワーが必要な場合は、バス ドライバーには、デバイスに電源が適用されます。 それ以外の場合、バス ドライバーでは、デバイスと通信する必要があると、すぐに電力が適用されます。

電源オフ、standby、および休止状態から高速スタートアップに時間を実現するために、ベスト プラクティスの一覧は、次を参照してください。[システム起動時のパフォーマンスを向上させる](improving-system-startup-performance.md)します。

 

 




