---
title: DPC の概要
description: DPC の概要
ms.assetid: 10e8d0e7-c04a-4dca-853c-74c911f59341
keywords:
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a71650b6943d36e77daaf19244f086eb0fd882f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828215"
---
# <a name="introduction-to-dpcs"></a>DPC の概要





通常、ISR を持つすべてのドライバーは、割り込みドリブン i/o 操作の処理を完了するために、少なくとも1つの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンを持っています。 一般的な最下位レベルのドライバーの*DpcForIsr*または*customdpc*ルーチンは、次のことを行います。

-   ISR が処理を開始した i/o 操作の処理を完了します。

-   次の IRP をデキューして、ドライバーが処理を開始できるようにします。

-   可能であれば、現在の IRP を完了します。

複数のデータ転送が必要なため、または回復可能なエラーが検出されたため、現在の IRP を完了できないことがあります。 このような場合、 *DpcForIsr*または*customdpc*ルーチンは、通常、別の転送または最後の操作の再試行のいずれかについてデバイスを再プログラムします。

*DpcForIsr*または*customdpc*ルーチンは、IRQL ディスパッチ\_レベルで任意の dpc コンテキストで呼び出されます。 ディスパッチ\_レベルで実行すると、 *DpcForIsr*または*customdpc*ルーチンが呼び出すことのできる一連のサポートルーチンが制限されます。 詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

DPC オブジェクトと Dpc は、タイマーでも使用できます。 詳細については、「 [Timer オブジェクトと dpc](timer-objects-and-dpcs.md)」を参照してください。

 

 




