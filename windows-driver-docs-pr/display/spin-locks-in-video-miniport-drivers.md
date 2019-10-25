---
title: ビデオ ミニポート ドライバーのスピン ロック
description: ビデオ ミニポート ドライバーのスピン ロック
ms.assetid: 89ec0139-c109-44b1-aadd-a909a19ca1ee
keywords:
- ビデオミニポートドライバー WDK Windows 2000、スピンロック
- スピンロック WDK ビデオミニポート
- WDK ビデオミニポートのロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468b886a0bc6d7650c7e41bed749ac7974f73840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825712"
---
# <a name="spin-locks-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーのスピン ロック


## <span id="ddk_spin_locks_in_video_miniport_drivers_gg"></span><span id="DDK_SPIN_LOCKS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


ビデオポートドライバーは、1つまたは複数のミニポートドライバースレッドが IRQL ディスパッチ\_レベルで実行されている場合に、データを保護するためのスピンロック関数を提供することで、ビデオミニポートドライバーでマルチプロセッサ同期をサポートします。 ビデオポートドライバーのスピンロック関数を使用すると、ミニポートドライバーのスレッドがスピンロックの作成、取得、解放、および破棄を行うことができます。 ビデオミニポートドライバーの作成者はビデオポートドライバーによってのみ提供される関数を使用してミニポートドライバーを実装する必要があるため、ビデオポートドライバーはこれらの機能を提供します。 スピンロックに関する一般的な説明については、「[スピンロック](https://docs.microsoft.com/windows-hardware/drivers/kernel/spin-locks)」を参照してください。

ビデオミニポートドライバーがスピンロックを使用できるようにするには、その前に[**Videoportcreatを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatespinlock)使用してスピンロックを作成する必要があります。 スピンロックが作成されると、スレッドは[**VideoPortAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570175)または[**VideoPortAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570176)のいずれかの呼び出しによって、スピンロックを取得しようとすることができます。 このペアの最初の関数は、ミニポートドライバーのスレッドが IRQL ディスパッチ\_レベル以下である場合に使用できます。 2番目の関数は、スレッドが IRQL ディスパッチ\_レベルで実行されている場合にのみ使用できます。

スピンロックを保持しているスレッドがタスクを完了すると、ミニポートドライバーによってスピンロックが解除されます。 スレッドが**VideoPortAcquireSpinLock**の呼び出しでスピンロックを取得した場合は、 [**videoportreleasespinlock**](https://msdn.microsoft.com/library/windows/hardware/ff570357)ロックを使用してスピンロックを解除する必要があります。 **Videoportreleasespinlock ロック**の呼び出しでは、スレッドは、その関数が返されたときに、 **VideoPortAcquireSpinLock**の*oldirql*パラメーターで受け取った*NewIrql*パラメーターで同じ値を渡す必要があります。 スレッドが**VideoPortAcquireSpinLockAtDpcLevel**を呼び出した場合は、 [**VideoPortReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570358)を呼び出して、スピンロックを解放する必要があります。

ミニポートドライバーがスピンロックに対してそれ以上使用しない場合は、 [**Videoportdeletespinlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportdeletespinlock)を呼び出すことによって、スピンロックを破棄する必要があります。

 

 





