---
title: 待機/ウェイク コールバック ルーチン
description: 待機/ウェイク コールバック ルーチン
ms.assetid: 55749f14-37eb-45d9-8a2c-9ebf7fb3bc75
keywords:
- 送信待機/ウェイク Irp
- Irp WDK の電源管理のウェイク/待機を送信します。
- コールバック ルーチン WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c69105b004673ec78e663e8415e74b98e0a1a54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571180"
---
# <a name="waitwake-callback-routines"></a>待機/ウェイク コールバック ルーチン





ドライバーは、待機/ウェイク IRP を要求するときに、ウェイク アップ イベントが発生した場合は作業の状態 (D0) にデバイスが返すことができます、コールバック ルーチンを指定する必要があります。 システムに渡されるコールバック ルーチンを呼び出すと、ウェイク アップ イベントが発生するし、すべてのドライバーは IRP を完了した、 [ **PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)します。

IRP で発生したドライバーの代わりにこのコールバック ルーチンが設定されているため、IRP を処理しているドライバーではなく — 呼び出さないでください[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776); のみ、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンのドライバーが IRP が下位のスタックを渡すように設定が [次へ] のパワー IRP を開始する必要があります。 ポリシー所有者はだけでなく、IRP を送信しますが、それを処理し、したがって設定可能性がありますに注意してください、 *IoCompletion*ルーチンの下位のスタック待機/ウェイク IRP を要求するときにコールバック ルーチンを設定するだけでなく IRP が渡されます。

コールバック ルーチンでは、次の責任があります。

1.  ドライバーが 1 つ以上のデバイスを管理している場合は、ウェイク アップをシグナル状態のデバイスのこれを決定します。

2.  ウェイク アップのシグナルを発生させたイベントのサービスを提供します。

3.  呼び出すことで、d0 でウェイク アップの通知デバイスを設定[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)を送信する、 **PowerDeviceD0**要求。 ドライバーは呼び出す必要がありますも[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)新しいデバイスの電源状態の電源マネージャーに通知します。 詳細については、[送信 IRP\_MN\_クエリ\_電源や IRP\_MN\_設定\_デバイスの電源状態のための電力](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)を参照してください。

4.  ドライバーを設定する場合、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) IRP、呼び出しの日常的な[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)をリセットする、 *キャンセル*ルーチンを**NULL**します。

5.  ドライバーには、複数のデバイスの電源ポリシーが所有している場合は、その待機/ウェイク参照カウントをデクリメントします。 カウントが 0 以外の場合は、別の待機またはスリープ解除 IRP を要求する別のデバイスが以前に送信待機/ウェイク IRP を示す (**PoRequestPowerIrp**) の PDO をします。

    たとえば、PCI デバイスには、待機/ウェイク アップ モデムとネットワーク インターフェイス カード (NIC) の両方を有効になっている場合があります。 NIC (したがって IRP の完了)、システムのスリープを解除する場合 PCI FDO は、モデムはウェイク アップできるように自体に別の待機またはスリープ解除 IRP を送信する必要があります。

待機/ウェイク IRP のコントロールを要求したドライバーの電源ポリシーがデバイス スタックをために、IRP の完了時に、そのデバイスを動作状態に返されます。 です。 下位のドライバーが既にが物理的に power デバイスに適用が、ポリシーの所有者を呼び出す必要があります**PoRequestPowerIrp**を送信する、 **IRP\_MN\_設定\_POWER** D0 デバイスの電源状態を要求します。 デバイス スタックのすべてのドライバーにはこの電源投入 IRP が処理された後にのみがこのデバイスは稼働状態に返されます。

 

 




