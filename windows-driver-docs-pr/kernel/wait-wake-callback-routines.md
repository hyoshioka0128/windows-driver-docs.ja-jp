---
title: 待機/ウェイクコールバックルーチン
description: 待機/ウェイクコールバックルーチン
ms.assetid: 55749f14-37eb-45d9-8a2c-9ebf7fb3bc75
keywords:
- 待機/ウェイク Irp の送信
- 待機/ウェイク Irp WDK 電源管理、送信
- コールバックルーチン WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c30347bf10b25e9a19a06d225e018dce2db47946
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838324"
---
# <a name="waitwake-callback-routines"></a>待機/ウェイクコールバックルーチン





ドライバーは、待機/ウェイク IRP を要求するときに、ウェイクアップイベントが発生したときにデバイスを動作状態 (D0) に戻すことができるように、コールバックルーチンを指定する必要があります。 ウェイクアップイベントが発生し、すべてのドライバーが IRP を完了すると、システムは[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)に渡されたコールバックルーチンを呼び出します。

このコールバックルーチンは IRP を開始したドライバーの代わりに設定されるため、IRP を処理するドライバーではなく、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp); を呼び出すことはできません。ドライバーとして設定された[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンだけが irp を停止すると、スタックは次の電源 irp を開始します。 ポリシーの所有者が IRP を送信するだけで処理を処理するわけではないことに注意してください。したがって、待機/ウェイク IRP を要求するときにコールバックルーチンを設定するだけでなく、IRP をスタックに渡すときに*Iocompletion*ルーチンが設定されることに注意してください。

コールバックルーチンには、次の役割があります。

1.  ドライバーが複数のデバイスを制御する場合は、どのデバイスがウェイクアップを通知するかを決定します。

2.  ウェイクアップシグナルの原因となったイベントをサービスします。

3.  [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して**PowerDeviceD0**要求を送信し、D0 状態でウェイクアップを通知するデバイスを設定します。 また、ドライバーは[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、新しいデバイスの電源状態を電源マネージャーに知らせる必要があります。 詳細については、「 [\_電力または\_irp を送信する irp\_\_クエリを実行する」を参照してください。デバイスの電源状態に\_電力を設定](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)します。\_

4.  ドライバーが IRP の[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを設定している場合は、 [**iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出して、*キャンセル*ルーチンを**NULL**にリセットします。

5.  ドライバーが複数のデバイスの電源ポリシーを所有している場合は、待機/ウェイク参照カウントをデクリメントします。 カウントが0以外の場合、別のデバイスが以前に待機/ウェイクアップ IRP を送信したことを示している場合は、その PDO に対して別の待機/ウェイク IRP (**PoRequestPowerIrp**) を要求します。

    たとえば、PCI デバイスでは、モデムとネットワークインターフェイスカード (NIC) の両方で待機/ウェイクが有効になっている場合があります。 NIC がシステムをスリープ解除する (したがって IRP を完了する) 場合、PCI FDO は、モデムが引き続きウェイクアップできるように、別の待機/ウェイク IRP をそれ自体に送信する必要があります。

待機/ウェイク IRP を要求したドライバーは、デバイススタックの電源ポリシーを制御するため、IRP の完了時にデバイスを動作状態に戻す役割を担います。 低いドライバーでは、デバイスに物理的に電力が供給されている場合がありますが、ポリシーの所有者は**PoRequestPowerIrp**を呼び出して、デバイスの電源状態の D0 に対する**電源要求\_\_設定**された IRP\_送信する必要があります。 デバイススタック内のすべてのドライバーがこの電源オン IRP を処理した後にのみ、デバイスが動作状態に戻ります。

 

 




