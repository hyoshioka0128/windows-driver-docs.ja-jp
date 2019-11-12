---
title: デバイスの電源切断 IRP の処理
description: デバイスの電源切断 IRP の処理
ms.assetid: 2f4591d6-5bd0-45db-b02d-cf9dd59c3888
keywords:
- パワー Irp WDK カーネル
- デバイスセットの電源 Irp WDK カーネル
- 電源 Irp WDK カーネル、デバイスの変更
- 電源ダウン Irp WDK カーネル
- コンテキスト情報 WDK の電源管理
- 電源管理のシャットダウン WDK カーネル
- オフパワー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad22502b48cb6b1f509cee8b32008794f9c60c1d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836588"
---
# <a name="handling-device-power-down-irps"></a>デバイスの電源切断 IRP の処理





デバイスの電源を切る IRP は、 [ **\_\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)とデバイスの電源状態 (**PowerDeviceD0**、 **PowerDeviceD1**、 **POWERDEVICED2**、または**PowerDeviceD3**) に設定されたマイナー関数コードの irp\_を指定します。電力が低いか、現在のデバイスの電源状態に等しい。 IRP がデバイススタックを移動するときに、ドライバーは電源を入れて IRP を処理する必要があります。 上位レベルのドライバーは、下位レベルのドライバーの前に、IRP を処理する必要があります。 デバイス固有のタスクを実行しないドライバーは、IRP を次の下位のドライバーに直ちに渡す必要があります。

次の図は、このような IRP の処理に関連する手順を示しています。

![デバイスの電源を切る要求の処理を示す図](images/devd3.png)

IRP で**PowerDeviceD3**が指定されている場合、関数ドライバーは通常、次のタスクを実行する必要があります。

-   現在の IRP を渡して[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、ドライバーが PnP\_irp を受信していないことを確認します。これにより、電源 irp の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了してから、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは**IoCompleteRequest**を呼び出して IRP を完了し、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して次の電源 irp を開始してから、エラーの状態を返します。

-   デバイスの電源を切断する前に実行する必要があるデバイス固有のタスクを実行します。たとえば、デバイスを閉じる、保留中の i/o を完了またはフラッシュする、割り込みを無効にする、[後続の受信 irp をキュー](queuing-i-o-requests-while-a-device-is-sleeping.md)に保存する、デバイスコンテキストを保存するなどの操作を行います。デバイスを復元または再初期化します。

    IRP を処理するときに、ドライバーで長い遅延が発生しないようにする必要があります (たとえば、ユーザーがこの種のデバイスに対して不適切である可能性がある遅延)。

    ドライバーは、デバイスが動作状態に戻るまで、着信 i/o 要求をキューに挿入する必要があります。

-   場合によっては、パラメーターの値を確認します。 **ShutdownType**. システムの set-power IRP がアクティブである場合、 **Shutdowntype**はシステムの irp に関する情報を提供します。 この値の詳細については、「[システム電源動作](system-power-actions.md)」を参照してください。

    休止状態のデバイスのドライバーは、この値を検査する必要があります。 **Shutdowntype**が**poweractionhibernate**の場合、ドライバーは、デバイスを復元するために必要なすべてのコンテキストを保存する必要がありますが、デバイスの電源を切ることはできません。

-   デバイスの物理電源の状態を変更することができる場合は、その変更が適切であるかどうかを変更します。

-   [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、新しいデバイスの電源状態を電源マネージャーに通知します。

-   [**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出して、次に小さいドライバーのスタック位置を設定します。

-   ドライバーが次の電源 IRP を処理する準備ができていることを示す[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出す*iocompletion*ルーチンを設定します。 Windows 7 と Windows Vista では、この手順は必要ありません。

-   Windows 7 と windows Vista で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出します。または、 [**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。 Irp は、IRP を完了するバスドライバーに渡す必要があります。

-   [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、以前に取得したロックを解放します。

-   ステータスを返す\_保留中です。

ドライバーは、すべてのデバイスコンテキスト情報を保存し、IRP を転送する前に新しい電源状態を設定する必要があります。 コンテキスト情報には、少なくとも要求された新しい電源状態が含まれている必要があります。 また、電源投入時にドライバーが必要とする追加情報も含まれている必要があります。 IRP が完了し、デバイスの電源がオフになると、ドライバーはデバイスにアクセスできなくなり、デバイスコンテキストを使用できなくなります。

各ドライバーは、IRP を次の下位のドライバーに渡す必要があります。 IRP がバスドライバーに到達すると、バスドライバーはデバイスを電源オフにし (この機能が可能な場合)、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して電源マネージャーに通知し、irp を完了します。

ただし、バスドライバーが休止状態のデバイスをサービスしている場合は、IRP の**Shutdowntype**の値が PowerSystemHibernate であるかどうかを確認する必要があります。 その場合、バスドライバーは**PoSetPowerState**を呼び出して PowerDeviceD3 を報告する必要がありますが、デバイスの電源を切ることはできません。 休止状態ファイルが保存された後、システムの残りの部分と共に、デバイスの電源が切断されます。

すべての子デバイスの電源を切った後、バスドライバーでもバスの電源を切ることができます。 このような動作は、デバイスに依存します。

IRP で他の状態 (D0、D1、または D2) が指定されている場合、必要なドライバーアクションはデバイスに依存します。 通常、これらの状態をサポートするデバイスは、i/o 要求が到着するとすぐに動作状態に戻ることができます。 このようなデバイスのドライバーは、保留中の i/o 要求を完了し、新しい要求をキューに格納して、必要なすべてのコンテキストを保存してから、IRP を次の下位のドライバーに転送する必要があります。 IRP がバスドライバーに到達すると、要求された状態のハードウェアが設定されます。 ドライバーは、スリープ状態のときにデバイスにアクセスできません。

場合によっては、関数またはフィルタードライバーが、デバイスが既に D0 状態にあるときに PowerDeviceD0 を指定するデバイスの電源 IRP を受け取ることがあります。 この IRP は、他の set-power IRP と同様に処理する必要があります。保留中の i/o 要求を完了し、受信 i/o 要求をキューに入れ、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定して、irp を次の下位のドライバーに渡します。 ただし、ドライバーでは、デバイスのハードウェア設定を変更することはできません。 バスドライバーが IRP を受け取ると、IRP を完了するだけです。 IRP が完了すると、関数ドライバーとフィルタードライバーは、キューに置かれた要求を処理できます。 IRP が完了するまで i/o をキューに登録すると、より高いドライバーで i/o を試行している間に、ドライバーがデバイスレジスタを変更しようとする可能性がなくなります。

 

 




