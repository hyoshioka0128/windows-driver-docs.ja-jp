---
title: IoTimer コンテキスト情報の提供
description: IoTimer コンテキスト情報の提供
ms.assetid: a92a7c3d-1602-430b-8ae1-c79bfc9ac7f9
keywords:
- IoTimer
- IoInitializeTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b52cdcd597811f2eb099992df30a41611396b9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838483"
---
# <a name="providing-iotimer-context-information"></a>IoTimer コンテキスト情報の提供





[**Ioinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)に渡される*コンテキスト*ポインターによって、他のドライバールーチンや[*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチン自体が、時間のかかる操作に関する状態を維持できるコンテキスト領域が識別されます。 I/o マネージャーは、 *Iotimer*ルーチンを呼び出すたびに*コンテキスト*ポインターを渡します。

*Iotimer*ルーチンは IRQL = ディスパッチ\_レベルで実行されるため、そのコンテキスト領域は常駐システム領域のメモリ内に存在する必要があります。 *Iotimer*ルーチンを含むほとんどのドライバーは、関連付けられているデバイスオブジェクトの[デバイス拡張機能](device-extensions.md)を*コンテキスト*アクセス可能な領域として使用しますが、ドライバーが[コントローラーオブジェクト](using-controller-objects.md)を使用する場合は、代わりにコンテキストをコントローラー拡張機能に含めることができます。ドライバーによって割り当てられた非ページプール。

*Iotimer * * * ルーチンのコンテキスト領域***については、次のガイドラインに従って**ください:*

-   *Iotimer*ルーチンが、そのコンテキスト領域をドライバーの ISR と共有する場合、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、マルチプロセッサセーフな方法でコンテキスト領域にアクセスする[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを呼び出す必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

-   *Iotimer*ルーチンがコンテキスト領域を ISR と共有せず、別のドライバールーチンと共有する場合、ドライバーは、のコンテキスト情報にアクセスするために、初期化された executive スピンロックを使用して共有コンテキスト領域を保護する必要があります。マルチプロセッサ-セーフな方法。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

 

 




