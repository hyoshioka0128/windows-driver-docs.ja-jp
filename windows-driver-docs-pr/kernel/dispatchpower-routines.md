---
title: DispatchPower ルーチン
description: DispatchPower ルーチン
ms.assetid: e385064f-cbdb-432f-951a-743217891333
keywords:
- ディスパッチルーチン WDK カーネル、DispatchPower ルーチン
- DispatchPower ルーチン
- 電源管理 WDK カーネル、ディスパッチルーチン
- IRP_MJ_POWER i/o 関数のコード
- リムーバブルデバイスの電源ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f74cc9d6ce51e119b8ca8e5a07b028212a2c5fd6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838728"
---
# <a name="dispatchpower-routines"></a>DispatchPower ルーチン





ドライバーの[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)I/o 関数コードの irp を処理することによって、[電源管理](implementing-power-management.md)をサポートします。 **IRP\_MJ\_power** functions コードに関連付けられているのは、電源管理用のいくつかのマイナー i/o 関数コードです。 電源マネージャーは、これらのマイナー関数コードを使用して、電源状態の変更、システムウェイクアップイベントの待機と応答、およびデバイスに関するドライバーの照会を行います。

各ドライバーの*DispatchPower*ルーチンは、次のタスクを実行します。

-   可能であれば、IRP を処理します。

-   [**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を使用して、IRP をデバイススタック内の次に小さいドライバーに渡します。

-   バスドライバーの場合は、要求された電源操作をデバイスで実行し、IRP を完了します。

デバイスのすべてのドライバーには、デバイスの電源 Irp を処理する機会が必要です。ただし、関数またはフィルタードライバーが IRP を失敗させることが許可されている場合は例外です。 ほとんどの関数およびフィルタードライバーは、何らかの処理を実行するか、各電源 IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定してから、irp を完了せずに次の下位のドライバーに渡します。 IRP は、必要に応じて物理的にデバイスの電源状態を変更し、IRP を完了するバスドライバーに到達します。

IRP が完了すると、i/o マネージャーは、IRP がデバイススタックを移動したときにドライバーによって設定された*Iocompletion*ルーチンを呼び出します。 ドライバーが完了ルーチンを設定する必要があるかどうかは、IRP の種類とドライバーの個々の要件によって異なります。

デバイスの電源をオンにする電源の Irp は、デバイススタックの最低ドライバー (基になるバスドライバー) によって最初に処理され、その後、各ドライバーがスタックを起動します。 デバイスの電源を切断する電源 Irp は、デバイススタックの一番上にあるドライバーによって最初に処理される必要があります。その後、後続の各ドライバーがスタックを停止します。

### <a name="special-handling-for-removable-devices"></a>リムーバブルデバイスの特別な処理

*DispatchPower*ルーチンでは、リムーバブルデバイスのドライバーは、デバイスがまだ存在しているかどうかを確認する必要があります。 デバイスが削除されている場合、ドライバーは IRP を次の下位のドライバーに渡すことはできません。 代わりに、ドライバーは次の操作を行う必要があります。

-   [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、次の電源 IRP の処理を開始します。

-   **Irp-&gt;iostatus. status**を status に設定し\_削除\_保留中です。

-   [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出し、IRP を完了するための IO\_\_の増分値を指定します。

-   状態を返す\_削除\_保留中です。

 

 




