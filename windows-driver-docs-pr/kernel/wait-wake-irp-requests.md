---
title: 待機/ウェイク IRP 要求
description: 待機/ウェイク IRP 要求
ms.assetid: c67d6dcb-f4a9-4df0-abb8-9d84fc44ec40
keywords:
- 待機/ウェイク Irp の送信
- ウェイクアップシグナルが有効になっている WDK カーネル
- 待機/ウェイク Irp WDK 電源管理、送信
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4775a1efd8115fbd73aa46d750dbf1cecf42f1b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835795"
---
# <a name="waitwake-irp-requests"></a>待機/ウェイク IRP 要求





[**IRP\_\_待機\_ウェイクアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)を送信するには、ドライバーは[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出し、ターゲット PDO へのポインター、システムの電源状態、コールバックルーチンへのポインターを渡します。

システム電源の状態は、この IRP がシステムをスリープ解除できる最小電力状態を指定します。 値は、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造の[**systemwake**](systemwake.md)状態と同じかそれ以上である必要があります。 たとえば、ドライバーが IRP に**PowerSystemSleeping2**を渡すと、関連する irp によってシステムが状態 S0、S1、S2 から復帰する可能性があります。 このような場合、システムは S0 と S2 (範囲内で最高および最低の状態) をサポートする必要がありますが、S1 はサポートしていません。

待機/ウェイク IRP を要求するすべてのドライバーは、他のすべてのドライバーが IRP を完了した後に呼び出される[コールバックルーチン](wait-wake-callback-routines.md)を指定する必要があります。 このルーチンでは、ドライバーは、デバイスを動作状態に戻すために必要な操作を実行できます。

**PoRequestPowerIrp**への応答として、電源管理者は、マイナーコード IRP を使用して電源 irp を **\_し\_待機\_ウェイク**し、ターゲット PDO のデバイススタックの一番上に送信します。 呼び出し元は、割り当てられた IRP へのポインターを返します。これは、後で IRP をキャンセルする必要がある場合に使用できます。

エラーが発生しなかった場合、 **PoRequestPowerIrp**は STATUS\_PENDING を返します。 この状態は、IRP が正常に送信され、完了待ちになっていることを意味します。

待機/ウェイク IRP は、システムまたはデバイスの電源状態を変更しません。 デバイスのウェイクアップシグナルを有効にするだけです。 IRP は、外部シグナルによってシステムまたはデバイスが停止するまで保留状態のままになります。

 

 




