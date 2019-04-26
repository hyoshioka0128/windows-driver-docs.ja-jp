---
title: DPC の概要
description: DPC の概要
ms.assetid: 10e8d0e7-c04a-4dca-853c-74c911f59341
keywords:
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990e4151becb3d9a7bbee1b9ef303a542bd5795b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341029"
---
# <a name="introduction-to-dpcs"></a>DPC の概要





通常 ISR を持つ任意のドライバーもに 1 つ以上[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)の処理を完了させるルーチン割り込み駆動の I/O 操作。 一般的な最下位レベル ドライバーの*DpcForIsr*または*CustomDpc*ルーチンは、次を実行します。

-   ISR が処理を開始したこと、I/O 操作の処理を終了します。

-   ドライバーは処理を開始できるように、[次へ] の IRP でデキューします。

-   可能であれば、現在の IRP を完了します。

場合によっていくつかのデータ転送が必要なまたは回復可能なエラーが検出されました現在 IRP を完了できません。 このような場合、 *DpcForIsr*または*CustomDpc*ルーチンが別の転送または最後の操作の再試行のいずれかのデバイスを通常 reprograms します。

A *DpcForIsr*または*CustomDpc*ルーチンは、IRQL のディスパッチに任意の DPC コンテキストで呼び出される\_レベル。 ディスパッチで実行されている\_レベル サポート ルーチンのセットを制限する、 *DpcForIsr*または*CustomDpc*ルーチンを呼び出すことができます。 参照してください[を管理するハードウェアの優先順位](managing-hardware-priorities.md)詳細についてはします。

DPC オブジェクトと Dpc は、タイマーにも使用できます。 詳細については、次を参照してください。[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)します。

 

 




