---
title: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
description: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
ms.assetid: 752b6c3c-f42a-469d-8a43-0778ecbe4541
keywords:
- 待機/ウェイク Irp の受信
- 待機/ウェイク Irp WDK 電源管理、受信
- 関数ドライバー WDK の電源管理
- FDOs WDK の電源管理
- DOs WDK 電源管理のフィルター処理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45bfc9ca693c6139d389065a2afaafbf0ba69965
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838674"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理





FDO またはフィルターを作成するドライバーが[**irp\_を\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)して、関連する PDO に対して\_ウェイクアップ要求を待機している場合は、irp を次の下位のドライバーに渡すか、irp を渡す前に特定のアクションを実行することができます。

### <a name="for-devices-that-support-wake-up"></a>ウェイクアップをサポートするデバイスの場合

待機/ウェイク IRP を受信したら、関数またはフィルタードライバーは次の手順を実行する必要があります。

1.  現在の IRP を渡して[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、ドライバーが PnP\_irp を受信していないことを確認します。これにより、待機/ウェイク IRP の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了し、エラー状態を返します。

2.  **PowerState の&gt;** 値を調べて、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造で、現在のデバイスの電源状態と**devicestate**\[systemwake\] を比較します。

    デバイスがウェイクアップをサポートしていても、指定した[Systemwake](systemwake.md)状態からではなく、現在のデバイスの電源状態からのものではない場合、ドライバーは次のように IRP を失敗させる必要があります。

    -   状態\_無効\_デバイス\_状態が**Irp-&gt;IoStatus. STATUS**に設定されています。
    -   IRP (**IoCompleteRequest**) を完了します。 IO の priority boost\_\_増分は指定しません。
    -   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから、 **Irp-&gt;iostatus. status**に設定されている状態を返します。

3.  それ以外の場合は、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を使用して、IRP の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。 *Iocompletion*ルーチンは、デバイスを動作状態に戻すためにドライバーが必要とするすべてのタスクを実行する必要があります。

    また、IRP が取り消された場合にも、 *Iocompletion*ルーチンが呼び出されます。

4.  *Iocompletion*ルーチンでドライバーが必要とする可能性のある情報をすべて保存します。

5.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 と windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 003、Windows XP、および windows 2000) を呼び出して、待機/ウェイク IRP を次の下位のドライバーに渡します。

6.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、以前に取得したロックを解放します。

7.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから STATUS\_PENDING が返されます。 Irp を保持しているときに、ドライバーが**irp-&gt;iostatus. Status**の値を変更することはできません。

### <a name="for-devices-that-do-not-support-wake-up"></a>ウェイクアップをサポートしていないデバイスの場合

関数またはフィルタードライバーがウェイクアップをサポートしていないデバイスに対して wait/wake IRP を受信した場合、ドライバーは次のように IRP を失敗させる必要があります。

1.  IRP (**IoCompleteRequest**) を完了します。 IO の priority boost\_\_増分は指定しません。

2.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから、 **Irp-&gt;iostatus. status**に設定されている状態を返します。

 

 




