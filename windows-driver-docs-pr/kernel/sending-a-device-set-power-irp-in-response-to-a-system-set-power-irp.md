---
title: システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信
description: システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信
ms.assetid: b2029292-d770-4095-8bd7-9358b282216c
keywords:
- set-パワー Irp の送信
- パワー Irp WDK 電源管理の設定
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d149b7fcf21c3f242a13dd990ca11b0aaf25109f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836374"
---
# <a name="sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp"></a>システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信





デバイスの電源ポリシー所有者は、次の手順を実行してシステムセット-電源 IRP に応答する必要があります。

1.  [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出し、現在の Irp を*タグ*パラメーターとして渡します。これにより、ドライバーがプラグアンドプレイ IRP\_を受信していないことを確認し、電源 irp の処理中に\_デバイス要求を[**削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)ます。

    **IoAcquireRemoveLock**がエラー状態を返した場合、ドライバーは IRP の処理を続行しません。 代わりに、Windows Vista 以降では、ドライバーは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して要求を完了してから、エラー状態を返す必要があります。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーはまず[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出し、 **IoCompleteRequest**を呼び出して IRP を完了してから、エラー状態を返します。

2.  [**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出して、次に低いドライバーの IRP スタックの場所を設定します。

3.  システムセット-power IRP で[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。

4.  [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、システム設定-電源 IRP を保留中としてマークします。

5.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows Vista 以降) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、システム設定-電源 IRP を次の下位のドライバーに渡します。

6.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)のルーチンから状態\_PENDING が返されます。

*Iocompletion*ルーチン (前の一覧の手順3を参照) で、デバイスの電源ポリシー所有者は、デバイスセット-電源 IRP を次のように送信します。

1.  システム設定-電源 IRP を調べて、要求されたシステム電源状態を取得します。 そのシステム電源状態に適したデバイスの電源状態を選択します。 詳細については、「[デバイスの電力の正しい状態の判断](determining-the-correct-device-power-state.md)」を参照してください。

2.  [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、手順 1. で確認したデバイスの電源状態に対して[ **\_電力\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_を送信します。 電源ポリシーの所有者は、デバイスが既にその状態にある場合でも、デバイスセット-電源要求を送信する必要があります。

3.  **PoRequestPowerIrp**の呼び出しで電源完了コールバックルーチン (*補完関数*) を指定し、*コンテキスト*バッファーにシステム設定-電源 IRP を渡します。

4.  *Iocompletion*ルーチンから要求される\_\_処理の状態を返します。これにより、ドライバーが電源完了コールバックルーチンでシステム設定-電源 IRP の処理を完了できるように\_ます。

デバイスの電源ポリシーの所有者は、デバイスセットを送信するだけでなく、デバイススタックを通過するときにもこの IRP を処理する必要があることに注意してください。 その結果、デバイスの電源ポリシー所有者は、デバイスセット-電源 IRP に関連付けられた電源完了コールバックルーチンと、システムセット-電源 IRP*の iocompletion* *ルーチンだけ*でなく、デバイスセット-電源 IRP。 詳細については、「[デバイスの電源状態の\_電力を設定する\_IRP\_を処理](handling-irp-mn-set-power-for-device-power-states.md)する」を参照してください。

I/o マネージャーは、デバイスセットとして設定されたすべての*Iocompletion*ルーチンを呼び出した後、デバイススタックを移動します。 i/o マネージャーは、電源完了コールバックルーチンを呼び出します。 この時点で、スタック内のすべてのドライバーがデバイスセット-電源 IRP を完了し、デバイスの電源の切り替えが完了しています。

電源完了コールバックルーチンは、次の操作を行う必要があります。

1.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、次の電源 IRP を開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

2.  システムの set-power IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了し、デバイスセット-電源 irp の状態を返します。

3.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、以前に取得したロックを解放します。

4.  セットパワー Irp が完了した状態を返します。

 

 




