---
title: 待機/ウェイク IRP の IoCompletion ルーチン
description: 待機/ウェイク IRP の IoCompletion ルーチン
ms.assetid: 61239398-2d37-4163-8128-7a4a0916a262
keywords:
- 待機/ウェイク Irp の受信
- 待機/ウェイク Irp WDK 電源管理、受信
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 367bf079156463522bfc64ebcf187efcccca6d3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838611"
---
# <a name="iocompletion-routines-for-waitwake-irps"></a>待機/ウェイク IRP の IoCompletion ルーチン





I/o マネージャーは、デバイススタック内の次の下位のドライバーが待機/ウェイク IRP を完了した後に、ドライバーの wait/wake [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを呼び出します。 待機/ウェイク IRP を処理する各関数とフィルター (FDO) ドライバーは、IRP の*Iocompletion*ルーチンを設定する必要があります。

各関数またはフィルタードライバーは、デバイススタックの下位にある待機/ウェイク IRP を処理するので、 *Iocompletion*ルーチンを設定します。 IRP を送信するデバイスの電源ポリシー所有者は、コールバックルーチンに加えて*Iocompletion*ルーチンを持つ場合があります。 このコールバックルーチンは*Iocompletion*ルーチンの後に呼び出され、2つの要件が異なることに注意してください。 詳細については、「 [Wait/Wake コールバックルーチン](wait-wake-callback-routines.md)」を参照してください。

待機/ウェイク*Iocompletion*ルーチンで必要な操作は、デバイスとドライバーの種類によって異なります。 次に、ドライバーが待機/ウェイク*Iocompletion*ルーチンで実行する必要があるいくつかの操作を示します。

1.  デバイス拡張機能の関連するフィールドをリセットします。 たとえば、待機/ウェイク IRP が保留中の場合、ほとんどのドライバーはフラグを設定し、デバイス拡張機能で IRP へのポインターを保持します。

2.  [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出し、ルーチンに**NULL**ポインターを指定して、IRP に対して[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが存在する場合は、そのルーチンをリセットします。

3.  **IoCompleteRequest**を呼び出し、IRP を完了するための IO\_\_の増分値を指定します。

連続した各ドライバーが IRP を完了すると、i/o マネージャーは、次に上位にあるドライバーの*Iocompletion*ルーチンに制御を渡してスタックをバックアップします。

ドライバーによって設定された*Iocompletion*ルーチンを呼び出した後、デバイススタックで待機/ウェイク IRP が渡されると、i/o マネージャーは、IRP を送信したドライバーによって[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)に渡されたコールバックルーチンを呼び出します。 詳細については、「 [Wait/Wake Callback ルーチン](wait-wake-callback-routines.md)」を参照してください。

 

 




