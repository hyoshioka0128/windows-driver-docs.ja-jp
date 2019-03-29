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
ms.openlocfilehash: 5d553192c89a9c699c65e5f7ab5eadc7197bd21f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571271"
---
# <a name="iocompletion-routines-for-device-power-irps"></a>デバイス電源 IRP の IoCompletion ルーチン





I/O マネージャーを呼び出す、バス ドライバーが IRP を完了したら、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP が渡されるときより高度なドライバーによって登録されたルーチンがスタックをダウンします。

各ドライバーの設定する必要があります、デバイス、D0 状態が入力、 *IoCompletion*稼働状態に戻すために必要な作業のほとんどを実行するルーチン。 ドライバーを設定する必要があります、 *IoCompletion* D0 状態へのすべての遷移の日常的なかどうか、デバイスから返されるスリープ状態またはシステムの起動時に D0 を入力します。 次の図は、タスクなど、 *IoCompletion*ルーチンを実行する必要があります。

![デバイスの電源投入 iocompletion ルーチンを示す図](images/d0-comp.png)

これらのタスクは次のとおりです。

-   デバイスの電源状態を復元またはとして、デバイスを再初期化が必要なおよびデバイスが稼働状態にいないときにドライバーによってキューに置かれたすべての I/O を処理する準備をしています

-   呼び出す[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765) D0 電源の状態、デバイスが電源マネージャーに通知します。

-   呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)ドライバーが IRP の現在の電源を最初に送信しなかった場合、[次へ] のパワー IRP を受信します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

-   デバイス コンテキストに割り当てられたメモリを解放します。

-   呼び出す[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)でドライバーが取得されたロックを解放するその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが受信したときに、IRP します。

-   状態を返す\_成功します。

バス ドライバーのデバイスを電源まで、または高いドライバーは、デバイスと通信する必要があります。

ドライバーを設定する必要があります、デバイスがスリープ状態になったとき、 *IoCompletion*ルーチンを呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) (の Windows Server 2003、Windows XP、および Windows2000 でのみ使用) し、削除ロックを解放します。 デバイスがスリープ状態中に、ドライバーがそのデバイスをアクセスできないことに注意してください。

 

 




