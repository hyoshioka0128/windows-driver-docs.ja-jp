---
title: デバイスの電源投入 IRP の処理
description: デバイスの電源投入 IRP の処理
ms.assetid: 8fcfd324-97f9-4fd0-8fa1-87685c6b5ec3
keywords:
- パワー Irp WDK カーネル
- デバイスセットの電源 Irp WDK カーネル
- 電源 Irp WDK カーネル、デバイスの変更
- 電源アップ Irp WDK カーネル
- スタートアップ電源管理 WDK カーネル
- パワー WDK カーネルを復元しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3215673ed79f35f45b6d0dd269718eded123eab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828313"
---
# <a name="handling-device-power-up-irps"></a>デバイスの電源投入 IRP の処理





デバイスの電源の Irp では、IRP\_が指定されています。これにより、[**電源\_電力が設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)され、現在のデバイスの電源状態よりも多くの電力を必要とするデバイスの電源状態が\_ます。 通常、電源の IRP は、デバイスの動作状態**PowerDeviceD0**を指定します。

デバイスの電源投入要求は、デバイスの基盤となるバスドライバーによって最初に処理される必要があります。その後、後続の各ドライバーがスタックをバックアップします。

次の図は、電源投入時の IRP の処理に関連する手順を示しています。

![デバイスの電源要求の処理を示す図](images/devd0.png)

IRP\_を処理するときに電源要求\_電源要求 **\_設定**する場合、関数またはフィルタードライバーは次の操作を行う必要があります。

-   [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出して、ドライバーが irp\_を受信していないことを確認します。これにより、電源投入時の irp の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了してから、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは**IoCompleteRequest**を呼び出して IRP を完了し、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して次の電源 irp を開始してから、エラーの状態を返します。

-   [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、保留中の IRP をマークします。

-   [**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出して、IRP スタックの場所を設定します。 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)のルーチンを設定した場合、ドライバーは**Ioskiplocation entiの場所**を呼び出すことができません。

-   [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して、電源オン*iocompletion*ルーチンを設定します。

    デバイスの電源投入時の IRP を処理する場合、ドライバーは*Iocompletion*ルーチンを設定してコンテキストを復元し、削除ロックを解除して、IRP の完了後にその他の必要なタスクを実行する必要があります。 ドライバーは、IRP が完了する前にコンテキストを復元しないでください。 詳細については、「[デバイスの電源 irp の Iocompletion ルーチン](iocompletion-routines-for-device-power-irps.md)」を参照してください。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 と windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。 IRP は、デバイススタックをバスドライバーに転送する必要があります。 バスドライバーのみが IRP を完了することが許可されています。

-   ステータスを返す\_保留中です。

バスドライバーが IRP を受信するときは、まず、デバイスがまだ存在していて、スリープ状態で削除または交換されていないことを確認する必要があります。 デバイスが存在しない場合、バスドライバーは親デバイスの[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出して、デバイスが消失したことをプラグアンドプレイマネージャーに通知する必要があります。 このような状況では、バスドライバーはデバイスの電源投入の IRP を失敗させる可能性があります。

デバイスがまだ存在する場合、バスドライバーは、デバイスを動作状態に戻すために必要なタスクを実行し、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して新しいデバイスの電源状態を電源マネージャーに通知し、IRP を完了します ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)). デバイスのスリープ中にドライバーの i/o がキューに置かれている場合、またはデバイスに突入電流電源が必要な場合は、バスドライバーによってデバイスに電力が適用されます。 それ以外の場合、バスドライバーはデバイスとの通信が必要になるとすぐに電力を適用します。

電源オフ、スタンバイ、および休止状態からの起動時間を短縮するためのベストプラクティスの一覧については、「[システム起動パフォーマンスの向上](improving-system-startup-performance.md)」を参照してください。

 

 




