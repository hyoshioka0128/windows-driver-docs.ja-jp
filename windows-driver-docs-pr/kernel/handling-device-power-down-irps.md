---
title: デバイスの電源切断 IRP の処理
description: デバイスの電源切断 IRP の処理
ms.assetid: 2f4591d6-5bd0-45db-b02d-cf9dd59c3888
keywords:
- セット power Irp WDK カーネル
- デバイスが電源 Irp WDK カーネルを設定
- 電源 Irp WDK カーネル、デバイスの変更
- Irp WDK カーネルの電源切断
- WDK の電源管理のコンテキスト情報
- シャット ダウンの電源管理の WDK カーネル
- WDK のカーネルを電源オフ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd5d33ad3429aa21260f2c3bfad0e06f63bafcb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386887"
---
# <a name="handling-device-power-down-irps"></a>デバイスの電源切断 IRP の処理





デバイスを電源オフ IRP がマイナー関数のコードを指定します[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)とデバイスの電源の状態 (**PowerDeviceD0**、 **PowerDeviceD1**、 **PowerDeviceD2**、または**PowerDeviceD3**) 以下を利用したまたは現在のデバイスの電源の状態と同じであります。 ドライバーは、デバイス スタックを通って IRP 電源 IRP を処理する必要があります。 高度なドライバーは IRP がドライバーの下位レベルの前に処理する必要があります。 実行するデバイスに固有のタスクを持たないドライバーでは、次の下位のドライバーに IRP を渡す必要があります速やかにします。

次の図では、このような IRP の処理に関連する手順を示します。

![デバイスの電源切断要求を処理するかを示す図](images/devd3.png)

IRP が指定されている場合**PowerDeviceD3**、関数ドライバーでは、次のタスクを実行する必要があります通常。

-   呼び出す[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を完了し、エラー状態を返します。 ドライバーが呼び出すサーバーの Windows Server 2003、Windows XP、および Windows 2000、 **IoCompleteRequest** IRP を完了するを呼び出すし[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)を開始する、IRP の電源を次に行い、エラー状態を返します。

-   行う必要がある、デバイスを閉じる、完了または保留中の I/O、いずれかのフラッシュなど、デバイスの電源が削除される前に、割り込みを無効にすると、デバイスに固有のタスクを実行[後続の受信 Irp のキュー](queuing-i-o-requests-while-a-device-is-sleeping.md)、およびデバイスの保存復元またはデバイスを再初期化するコンテキスト。

    ドライバーが長時間の遅延 (ユーザーがこの種類のデバイスの不合理あります遅延など) に発生することはできません、IRP の処理中にします。

    デバイスが稼働状態に戻ったまで、ドライバーはすべての I/O 要求をキューする必要があります。

-   場合によっての値を確認**Parameters.Power.ShutdownType**します。 システム設定 power IRP はアクティブである場合、 **ShutdownType** IRP システムに関する情報を提供します。 この値の詳細については、次を参照してください。[システム電源操作](system-power-actions.md)します。

    休止パス上のデバイスのドライバーでは、この値を検査する必要があります。 場合、 **ShutdownType**は**PowerActionHibernate**ドライバーは、デバイスを復元するために必要な任意のコンテキストを保存する必要がありますが、デバイスの電源する必要があります。

-   変更が適切な場合は、ドライバーではこれを行う場合とは、デバイスの物理的な電源状態を変更します。

-   呼び出す[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)新しいデバイスの電源状態の電源マネージャーに通知します。

-   呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)の次の下位ドライバー スタックの場所を設定します。

-   設定、 *IoCompletion*ルーチンを呼び出す[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)ドライバーが IRP の [次へ] のパワーを処理する準備ができてことを示します。 Windows 7 および Windows Vista では、この手順は必要はありません。

-   呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (Windows 7 および Windows Vista) の呼び出しまたは[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、および Windows で2000) をクリックし、次の下位ドライバーに IRP を渡す。 IRP が完了すると、バス ドライバーまで IRP を渡す必要があります。

-   呼び出す[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)以前に取得したロックを解除します。

-   状態を返す\_保留します。

ドライバーは、任意のデバイス コンテキスト情報を保存および IRP を転送する前に新しい電源の状態を設定する必要があります。 コンテキストについては、含めることは、少なくとも、要求された新しい電源の状態。 その他の情報の電源投入時に、ドライバーが必要がある必要があります。 IRP が完了すると、デバイスの電源が入っていない、ドライバーでは、デバイスがアクセスできなくでき、デバイス コンテキストは使用できません。

各ドライバーでは、次の下位のドライバーに IRP を渡す必要があります。 IRP では、バス ドライバーに達すると、バス ドライバーの電源オフ (この機能である) 場合、デバイスが呼び出し[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)電源マネージャーに通知する IRP が完了するとします。

ただし、チェックイン、休止状態のデバイスをサービス バス ドライバー場合かどうかの値**ShutdownType** IRP が PowerSystemHibernate します。 場合は、バス ドライバーを呼び出す必要がありますので、 **PoSetPowerState** PowerDeviceD3 がありませんが、レポートにデバイスを電源。 システムの残りの部分と共に、休止状態ファイルを保存した後、デバイスが電源します。

結局のところその子デバイスの電源ダウンには、バス ドライバーが、バスの電源をもことができます。 このような動作は、デバイスによって異なります。

IRP では、他の状態 (D0、D1 または D2) を指定する場合の必要なドライバー操作はデバイスに依存します。 通常、これらの状態をサポートするデバイスにすぐに戻し作業状態、I/O 要求が到着するとします。 このようなデバイス用のドライバーでは、保留中の I/O 要求を完了、新しい要求をキュー、および次の下位のドライバーに IRP を転送する前に必要なすべてのコンテキストを保存する必要があります。 IRP では、バス ドライバーに達すると、要求された状態で、ハードウェアを設定します。 スリープ中に、ドライバーは、デバイスにアクセスできません。

状況によっては、関数またはフィルター ドライバーがデバイスを受け取ることがあります、デバイスが既に D0 状態のときに、PowerDeviceD0 を指定する IRP の電源をします。 他の任意のセット power IRP のように、ドライバーがこの IRP を処理する必要があります保留中の I/O 要求を完了し、受信の I/O 要求をキュー、、の設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンと次の下位に IRP のパス。ドライバー。 ただし、ドライバーでは、デバイスのハードウェア設定を変更する必要があります、します。 バス ドライバーは IRP を受信すると、単に IRP を完了する必要があります。 IRP が完了したら、関数とフィルター ドライバーは、キューに置かれた要求を処理できます。 IRP が完了するまでキューの I/O は、以上のドライバーが I/O を試行中に、デバイスの登録を変更しようとしています。 下のドライバーの可能性を排除します。

 

 




