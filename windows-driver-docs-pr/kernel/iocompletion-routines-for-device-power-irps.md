---
title: デバイス電源 IRP の IoCompletion ルーチン
description: デバイス電源 IRP の IoCompletion ルーチン
ms.assetid: c275fcba-5fa9-427c-8d7e-2339563985e4
keywords:
- IoCompletion ルーチン
- 電源 Irp WDK カーネル、デバイスの変更
- 状態遷移の WDK 電源管理
- デバイスの状態遷移の WDK 電源管理
- 動作状態は、WDK の電源管理を返します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244c56d1fdd835fbb78e7c6dad3785c0f2a28aac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381690"
---
# <a name="iocompletion-routines-for-device-power-irps"></a>デバイス電源 IRP の IoCompletion ルーチン





I/O マネージャーを呼び出す、バス ドライバーが IRP を完了したら、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP が渡されるときより高度なドライバーによって登録されたルーチンがスタックをダウンします。

各ドライバーの設定する必要があります、デバイス、D0 状態が入力、 *IoCompletion*稼働状態に戻すために必要な作業のほとんどを実行するルーチン。 ドライバーを設定する必要があります、 *IoCompletion* D0 状態へのすべての遷移の日常的なかどうか、デバイスから返されるスリープ状態またはシステムの起動時に D0 を入力します。 次の図は、タスクなど、 *IoCompletion*ルーチンを実行する必要があります。

![デバイスの電源投入 iocompletion ルーチンを示す図](images/d0-comp.png)

これらのタスクは次のとおりです。

-   デバイスの電源状態を復元またはとして、デバイスを再初期化が必要なおよびデバイスが稼働状態にいないときにドライバーによってキューに置かれたすべての I/O を処理する準備をしています

-   呼び出す[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate) D0 電源の状態、デバイスが電源マネージャーに通知します。

-   呼び出す[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)ドライバーが IRP の現在の電源を最初に送信しなかった場合、[次へ] のパワー IRP を受信します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

-   デバイス コンテキストに割り当てられたメモリを解放します。

-   呼び出す[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)でドライバーが取得されたロックを解放するその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが受信したときに、IRP します。

-   状態を返す\_成功します。

バス ドライバーのデバイスを電源まで、または高いドライバーは、デバイスと通信する必要があります。

ドライバーを設定する必要があります、デバイスがスリープ状態になったとき、 *IoCompletion*ルーチンを呼び出す[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) (の Windows Server 2003、Windows XP、および Windows2000 でのみ使用) し、削除ロックを解放します。 デバイスがスリープ状態中に、ドライバーがそのデバイスをアクセスできないことに注意してください。

 

 




