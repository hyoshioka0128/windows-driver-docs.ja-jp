---
title: デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理
description: デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理
ms.assetid: 680e3be2-63d9-4d79-a7c0-422e852e9347
keywords:
- クエリ-電源 Irp の WDK 電源管理
- デバイスの電源ポリシー所有者 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64773b960d56742137fa923da852d4ebce48355d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838679"
---
# <a name="handling-a-system-query-power-irp-in-a-device-power-policy-owner"></a>デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理





デバイスの電源ポリシー所有者がシステム電源状態の[**irp\_\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)を受信すると、クエリを渡し、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンで irp\_完了した\_クエリを送信することによって応答し **@no__t_** デバイスの電源状態の場合は10_ パワー。 スタック内のすべてのドライバーがデバイスクエリを完了すると、デバイスの電源ポリシー所有者はシステムクエリを完了します。

デバイスの電源ポリシー所有者は、 [DispatchPower ルーチン](dispatchpower-routines.md)で次の手順を実行して、システムクエリに応答する必要があります。

1.  現在の IRP を渡して[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、ドライバーが PnP\_irp を受信していないことを確認します。これにより、電源 irp の処理中に[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了し、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出し、 **IoCompleteRequest**を呼び出して IRP を完了し、エラーの状態を返す必要があります。

2.  「[フィルターまたは関数ドライバーでのシステムクエリ-電源 IRP の失敗](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)」で説明されているように、ドライバーが照会されたシステムの電源状態をサポートできることを確認します。 それ以外の場合は、このセクションで説明されているように、エラー状態で IRP を完了します。

    ただし、デバイスのウェイクアップが有効になっていても、システムを休止状態から復帰させることができない場合は、S4 (**Powersystemhibernate**) に対するクエリがドライバーで失敗しないようにする必要があります。 この場合、ドライバーの電源ポリシー所有者 ( [**IRP\_\_wait\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) に送信して、待機/ウェイク IRP をキャンセルし、システムクエリを成功させる必要があります。 詳細については、「 [Wait/WAKE IRP のキャンセル](canceling-a-wait-wake-irp.md)」を参照してください。

3.  ドライバーがクエリされたシステムの電源状態をサポートできる場合は、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出します。

4.  [**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出して、次に低いドライバーの IRP スタックの場所を設定します。

5.  システムクエリの電源 IRP に*Iocompletion*ルーチンを設定します。

6.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 および windows Vista の場合) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。

7.  ステータスを返す\_保留中です。

[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、次の操作を行う必要があります。

1.  **Irp&gt;iostatus. status**を調べて、低いドライバーが irp を正常に完了したことを確認します。 下位のドライバーで、成功しない NTSTATUS 値が指定されている場合、 *Iocompletion*ルーチンは ntstatus 値を返す必要があります。

2.  低いドライバーが IRP を正常に完了した場合は、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、照会されたシステムの電源状態に対して有効なデバイスの電源状態のデバイスクエリを送信します。 必要に応じて、デバイスの[ **\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造でデバイス\_状態の配列を参照して、照会されたシステムの電源状態に対して有効なデバイスの電源状態を判断します。

3.  **PoRequestPowerIrp**の呼び出しでコールバックルーチン (*補完関数*パラメーター) を指定し、*コンテキスト*領域にシステム IRP を渡します。

4.  ドライバーがコールバックルーチンでシステムクエリの IRP の処理を完了できるようにするために必要な\_処理\_の状態\_返します。

IRP が完了し、IRP 処理中に設定されたすべての*Iocompletion*ルーチンが実行されると、電源マネージャーは、i/o マネージャーを介して、電源ポリシーマネージャーのコールバックルーチン ( **PoRequestPowerIrp**)。 さらに、コールバックルーチンは、次の操作を行う必要があります。

1.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、次の電源 IRP を開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

2.  システムクエリ-power IRP (call [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了して、デバイスのクエリ-電源 irp の状態を返します。

3.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、以前に取得したロックを解放します。

デバイスの電源ポリシーの所有者は、デバイスのクエリを送信するだけでなく、デバイスのスタック内でも処理する必要があることに注意してください。 詳細については、「[デバイスの電源状態の\_クエリ\_電力の IRP\_処理](handling-irp-mn-query-power-for-device-power-states.md)」を参照してください。

 

 




