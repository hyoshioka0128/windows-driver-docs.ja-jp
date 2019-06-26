---
title: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
description: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
ms.assetid: 752b6c3c-f42a-469d-8a43-0778ecbe4541
keywords:
- 受信側の待機またはスリープ解除 Irp
- 待機/ウェイク Irp WDK の電源管理の受信
- 関数のドライバー WDK の電源管理
- Fdo WDK の電源管理
- フィルター DOs WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03fca8ce3c33a7d4f65c0bce5f0f6da7c6c3e51b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384242"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理





FDO またはフィルターを作成するドライバーは受信すると、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP が単に渡すことができますか、関連付けられている PDO を要求して次の下位ドライバーまたは IRP を渡す前に特定のアクションを実行します。

### <a name="for-devices-that-support-wake-up"></a>ウェイク アップをサポートするデバイス

待機/ウェイク IRP を受信すると、関数またはフィルター ドライバーは、以下の手順を実行する必要があります。

1.  呼び出す[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)待機/ウェイク IRP の処理中に要求します。

    場合[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock) 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 IRP が完了する代わりに、([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest))、エラー状態を返すとします。

2.  値を検査**Irp -&gt;Parameters.WaitWake.PowerState**で現在のデバイスの電源状態を比較し、 **DeviceState**\[SystemWake\]で、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体。

    指定したから、デバイスが、ウェイク アップをサポートしている場合は[SystemWake](systemwake.md)状態または現在のデバイスの電源状態からではなく、ドライバーは IRP を失敗次のようにします。

    -   状態を設定\_無効な\_デバイス\_で状態**Irp -&gt;IoStatus.Status**します。
    -   IRP の完了 (**IoCompleteRequest**)、IO の優先順位を指定する\_いいえ\_インクリメントします。
    -   設定の状態を返す**Irp -&gt;IoStatus.Status**から、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

3.  それ以外の場合、設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP を使用して、日常的な[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)します。 *IoCompletion*ルーチンは、ドライバーは、デバイスを動作状態に戻す必要がありますすべてのタスクを実行する必要があります。

    *IoCompletion* IRP が取り消された場合、ルーチンを呼び出すことがもできます。

4.  ドライバーに必要なすべての情報を保存、 *IoCompletion*ルーチン。

5.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (Windows 7、Windows Vista で) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (で Windows Server 003、Windows XP、および Windows 2000)次の下位ドライバーには、待機/ウェイク IRP を渡す。

6.  呼び出す[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)以前に取得したロックを解除します。

7.  状態を返す\_から PENDING、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 ドライバーの値を変更する必要があります**Irp -&gt;IoStatus.Status** IRP を保持しています。

### <a name="for-devices-that-do-not-support-wake-up"></a>ウェイク アップをサポートしていないデバイス

関数またはフィルター ドライバー、待機/ウェイク IRP ウェイク アップをサポートしていないデバイスの場合、ドライバーは IRP を次のように、失敗。

1.  IRP の完了 (**IoCompleteRequest**)、IO の優先順位を指定する\_いいえ\_インクリメントします。

2.  設定の状態を返す**Irp -&gt;IoStatus.Status**から、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




