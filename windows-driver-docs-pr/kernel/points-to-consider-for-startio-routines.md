---
title: StartIo ルーチンの考慮事項
description: StartIo ルーチンの考慮事項
ms.assetid: 389240d0-682f-48b3-940f-c107e9f60155
keywords:
- StartIo ルーチン, StartIo ルーチンについて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f585110db8703aed00f198632b5d26eb8b08a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827670"
---
# <a name="points-to-consider-for-startio-routines"></a>StartIo ルーチンの考慮事項





[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを実装する場合は、次の点に注意してください。

-   *StartIo*ルーチンは、物理デバイスと共有状態情報、または同じデバイス、メモリ位置にアクセスするドライバーの他のルーチンを使用して、ドライバーによってデバイス拡張に保持されているリソースへのアクセスを同期する必要があります。参考.

    *StartIo*ルーチンがデバイスまたは状態を ISR と共有している場合は、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、デバイスをプログラムしたり、共有状態にアクセスしたりするために、ドライバーによって提供される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを呼び出す必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

    *StartIo*ルーチンが、ISR 以外のルーチンと状態またはリソースを共有する場合、ドライバーによって提供される、ドライバーで初期化された executive スピンロックを使用して、共有状態またはリソースを保護する必要があります。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

-   モノリシックな非 WDM デバイスドライバーがコントローラーオブジェクトを設定した場合、その*StartIo*ルーチンはコントローラーオブジェクトを使用して、接続された (類似した) デバイスを持つ共有物理デバイスを介して操作を同期できます。

    詳細については、「[コントローラーオブジェクト](using-controller-objects.md)」を参照してください。

-   密接に結合された上位レベルのドライバーが、その基になるデバイスドライバーに対して大きな DMA 転送要求を事前に行っていない限り、基になるデバイスドライバーの*StartIo*ルーチンは、大規模な転送要求を部分転送範囲に分割する必要があり、ドライバーは部分転送デバイス操作のシーケンスを実行します。 各部分転送は、ハードウェアの機能に合わせてサイズを調整する必要があります。これは、ドライバーのデバイスの機能、または下位 DMA デバイスの機能のいずれかで、システム DMA コントローラーの機能のうち、より厳密な制約があるものです。

    システムまたはバスマスタ DMA の使用の詳細については[、「アダプターオブジェクトと dma](adapter-objects-and-dma.md) 」を参照してください。

-   DMA を使用するドライバーの*StartIo*ルーチンは、[アダプターオブジェクト](adapter-objects-and-dma.md)を使用して転送を同期する必要があります。

-   *StartIo*ルーチンは、IRQL = ディスパッチ\_レベルで実行されます。これにより、呼び出し可能な一連のサポートルーチンが制限されます。

    たとえば、 *StartIo*ルーチンは、ページング可能なメモリにアクセスしたり割り当てたりすることはできません。また、ディスパッチャーオブジェクトがシグナル状態に設定されるのを待機することもできません。 一方、 *StartIo*ルーチンは、 [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)と[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)を使用してドライバーによって割り当てられた executive スピンロックを取得して解放することができ、 [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)よりも高速に実行されます。[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)。

    詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」および「[スピンロック](spin-locks.md)」を参照してください。

-   ドライバーが取り消し可能な状態の Irp を保持している場合、その*StartIo*ルーチンは、デバイス上でその要求の処理を開始する前に、入力 IRP が既にキャンセルされているかどうかを確認する必要があります。 詳細については、「 [irp のキャンセル](canceling-irps.md)」を参照してください。

 

 




