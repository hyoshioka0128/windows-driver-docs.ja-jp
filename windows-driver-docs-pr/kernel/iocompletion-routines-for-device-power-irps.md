---
title: デバイス電源 IRP の IoCompletion ルーチン
description: デバイス電源 IRP の IoCompletion ルーチン
ms.assetid: c275fcba-5fa9-427c-8d7e-2339563985e4
keywords:
- IoCompletion ルーチン
- 電源 Irp WDK カーネル、デバイスの変更
- 状態遷移 WDK 電源管理
- デバイスの状態遷移 WDK の電源管理
- 動作状態は WDK 電源管理を返します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b001f69ae04ec826deb611d93d62b00221999a39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828166"
---
# <a name="iocompletion-routines-for-device-power-irps"></a>デバイス電源 IRP の IoCompletion ルーチン





バスドライバーが IRP を完了すると、i/o マネージャーは、上位レベルのドライバーによって登録された[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが、スタックに渡されたときにそのルーチンを呼び出します。

デバイスが D0 状態になるたびに、各ドライバーは、動作状態に戻すために必要なほとんどのタスクを実行する*Iocompletion*ルーチンを設定する必要があります。 ドライバーは、デバイスがスリープ状態から復帰するか、システムの起動時に D0 に入っているかどうかにかかわらず、D0 状態への遷移に対して*Iocompletion*ルーチンを設定する必要があります。 次の図は、 *Iocompletion*ルーチンによって実行されるタスクを示しています。

![デバイスの電源投入 iocompletion ルーチンを示す図](images/d0-comp.png)

次のようなタスクがあります。

-   デバイスの電源状態を復元するか、必要に応じてデバイスを再初期化し、デバイスが動作状態でない間にドライバーによってキューに登録されている i/o を処理する準備をする

-   [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、デバイスが D0 の電源状態であることを電源マネージャーに通知します。

-   ドライバーが最初に現在の電源 IRP を送信しなかった場合は、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して次の電源 irp を受信します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

-   デバイスコンテキストに割り当てられたメモリを解放します。

-   [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、IRP を受信したときにドライバーが[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで取得したロックを解放します。

-   正常\_状態を返します。

バスドライバーは、デバイスがデバイスと通信する必要があるまで、デバイスの電源を入れません。

デバイスがスリープ状態になると、ドライバーは、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) (windows Server 2003、windows XP、および windows 2000 のみ) を呼び出す*iocompletion*ルーチンを設定し、削除ロックを解除する必要があります。 デバイスがスリープ状態の間は、ドライバーがそのデバイスにアクセスできないことに注意してください。

 

 




