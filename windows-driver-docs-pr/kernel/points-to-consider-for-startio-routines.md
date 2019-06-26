---
title: StartIo ルーチンの考慮すべき点
description: StartIo ルーチンの考慮すべき点
ms.assetid: 389240d0-682f-48b3-940f-c107e9f60155
keywords:
- StartIo ルーチンについての StartIo ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d322a35b05940750354b33b42b2970c9e76c066
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369705"
---
# <a name="points-to-consider-for-startio-routines"></a>StartIo ルーチンの考慮すべき点





実装する場合、次の点を留意してください、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。

-   A *StartIo*ルーチンは、物理デバイスへのアクセスを同期する必要があり、状態情報を共有するのにはいずれかまたはドライバーを使用したデバイスの拡張機能で、ドライバーを保持するリソースの同じデバイス、メモリにアクセスするその他のルーチン場所、またはリソースします。

    場合、 *StartIo*ルーチン ISR と、デバイスや状態を共有する、それを使用する必要があります[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出すドライバーによって提供される[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンまたは共有の状態にアクセスするデバイスをプログラミングします。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

    場合、 *StartIo*日常的な共有状態または ISR 以外のルーチンでリソースの場合は、共有状態またはドライバーが、記憶域を提供するドライバー初期化 executive スピン ロックでのリソースを保護にする必要があります。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

-   WDM 以外のモノリシックなデバイス ドライバーが、コント ローラー オブジェクトを設定する場合、 *StartIo*ルーチンは、コント ローラー オブジェクトを使用して、接続されている (と同様) デバイスと共有の物理デバイスで操作を同期します。

    参照してください[コント ローラー オブジェクト](using-controller-objects.md)詳細についてはします。

-   密接に結合されたより高度なドライバー presplits 大きな DMA 転送しない限り、要求の基になるデバイス ドライバーの場合、基になるデバイス ドライバーの*StartIo*ルーチンを使用して、大きな転送要求を転送部分に分割する必要があります範囲と、ドライバーは、部分転送デバイス操作のシーケンスを実行する必要があります。 各部分の転送は、ハードウェアの機能に合わせてサイズに設定する必要があります。 いずれかの機能のドライバーのデバイスや、下位の DMA デバイス、システムの DMA コント ローラーの機能より厳密な制約が存在する方。

    参照してください[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)詳細については、システムまたはバス マスター DMA を使用します。

-   *StartIo* DMA を使用するドライバーのルーチンを使用して転送を同期する必要があります、[アダプター オブジェクト](adapter-objects-and-dma.md)します。

-   A *StartIo* IRQL でルーチンを実行 = ディスパッチ\_レベルで、呼び出すことができますサポート ルーチンのセットを制限します。

    たとえば、 *StartIo*ルーチンはアクセスも、ページング可能なメモリの割り当てし、シグナル状態に設定するディスパッチャー オブジェクトを待つことはできません。 一方で、 *StartIo*ルーチンを取得しをドライバーに割り当てられた executive スピン ロックの解放[ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)と[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)これよりも高速実行[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)と[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)します。

    参照してください[を管理するハードウェアの優先順位](managing-hardware-priorities.md)と[スピン ロック](spin-locks.md)詳細についてはします。

-   キャンセル可能な状態で、ドライバーが Irp を保持している場合、 *StartIo*ルーチンが入力の IRP はデバイス上でその要求の処理を開始する前に既にキャンセルされているかどうかを確認する必要があります。 詳細については、次を参照してください。[キャンセル Irp](canceling-irps.md)します。

 

 




