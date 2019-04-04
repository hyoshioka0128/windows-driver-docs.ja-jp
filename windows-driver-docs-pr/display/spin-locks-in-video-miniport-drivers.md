---
title: ビデオのミニポート ドライバーでスピン ロック
description: ビデオのミニポート ドライバーでスピン ロック
ms.assetid: 89ec0139-c109-44b1-aadd-a909a19ca1ee
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、スピン ロック
- スピン ロック WDK のビデオのミニポート
- ロックの WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b69ca114bf6e01f930d8ad1dfdb80ee35000e6eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532135"
---
# <a name="spin-locks-in-video-miniport-drivers"></a>ビデオのミニポート ドライバーでスピン ロック


## <span id="ddk_spin_locks_in_video_miniport_drivers_gg"></span><span id="DDK_SPIN_LOCKS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


ビデオ ポート ドライバーは、ときに 1 つのデータを保護するスピン ロック機能を提供することで、ビデオのミニポート ドライバーでのマルチプロセッサ同期をサポートまたはミニポート ドライバー スレッドの詳細については、IRQL ディスパッチ以下で実行している\_レベル。 ビデオ ポート ドライバーのスピン ロック関数では、ミニポート ドライバー スレッドを作成、取得、リリース、および破棄スピン ロックを有効にします。 ビデオ ポート ドライバーは、ビデオのミニポート ドライバー作成者が排他的ビデオ ポート ドライバーによって提供される関数を使用して、ミニポート ドライバーを実装する必要があるために、これらの関数を提供します。 スピン ロックの概要については、[スピン ロック](https://msdn.microsoft.com/library/windows/hardware/ff563830)を参照してください。

呼び出して、スピン ロックを作成する必要があります、ビデオのミニポート ドライバーでは、スピン ロックを使用できます、前に[ **VideoPortCreateSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570289)します。 スレッドがいずれかへの呼び出しでスピン ロックの取得を試みることができますスピン ロックが作成されたら、 [ **VideoPortAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570175)または[ **VideoPortAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570176)します。 ミニポート ドライバーのスレッドは、IRQL ディスパッチ以下で、このペアの最初の関数を使用できる\_レベル。 2 番目の関数は IRQL ディスパッチでスレッドが実行されている場合にのみ使用できます\_レベル。

スピン ロックが保持しているスレッドには、そのタスクが完了したら、ミニポート ドライバーはスピン ロックを解放する必要があります。 スレッドがへの呼び出しでスピン ロックを取得したかどうか**VideoPortAcquireSpinLock**、どちらを使用する[ **VideoPortReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570357)スピン ロックを解除します。 呼び出しで**VideoPortReleaseSpinLock**、スレッドが同じ値を渡す必要があります、 *NewIrql*で受け取ったパラメーター、 *OldIrql* のパラメーター**VideoPortAcquireSpinLock**その関数が返されます。 スレッドが呼び出された場合**VideoPortAcquireSpinLockAtDpcLevel**を呼び出す必要が[ **VideoPortReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff570358)スピン ロックを解除します。

呼び出して、スピン ロックを破棄する必要がありますミニポート ドライバーにスピン ロックを使用してない場合は、 [ **VideoPortDeleteSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570293)します。

 

 





