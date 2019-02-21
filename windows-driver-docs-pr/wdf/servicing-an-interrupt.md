---
title: 割り込みを処理します。
description: 割り込みを処理します。
ms.assetid: b6306d2c-a7be-4fc3-8123-4d2b5c60c988
keywords:
- ハードウェアの割り込み処理の WDK KMDF
- WDK KMDF、サービスの中断します。
- 割り込み WDK KMDF
- 割り込みサービス ルーチン WDK KMDF
- Isr WDK KMDF
- 遅延プロシージャ呼び出しの WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea2f58ab9d26aaab66cc6b95d7e88243bddf9346
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537450"
---
# <a name="servicing-an-interrupt"></a>割り込みを処理します。


このトピックでは、DIRQL 割り込みを処理する方法を説明します。 パッシブ レベル割り込みを処理する方法の詳細については、次を参照してください。[パッシブ レベルをサポートしている中断](supporting-passive-level-interrupts.md#servicing)します。

割り込みをサービスは、2 つ、および場合によって 3 つの手順で構成されます。

1.  レジスタの内容) などの揮発性の情報を迅速に保存するには、IRQL で実行される割り込みサービス ルーチン = DIRQL います。

2.  IRQL で実行される遅延プロシージャ呼び出し (DPC) の保存された揮発性の情報を処理するディスパッチ =\_レベル。

3.  追加の作業を実行する IRQL = パッシブ\_レベルに必要な場合。

どのフレームワーク ベースのドライバーの実装として、ドライバーの割り込みサービス ルーチン (ISR) フレームワークをデバイスでは、ハードウェア割り込みを生成するとき、 [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数。

[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)などレジスタの内容、もう 1 つの割り込みが発生した場合に失われますが、デバイスの DIRQL、割り込みについては、簡単に保存する必要がありますで実行されるコールバック関数。

通常、 [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数が低いかどうかを後で保存された情報の処理に遅延プロシージャ呼び出し (DPC) をスケジュール (ディスパッチ\_レベル)。 フレームワーク ベースのドライバーと DPC ルーチンを実装する[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)コールバック関数。

ほとんどのドライバーを使用して、1 つ[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)割り込みの種類ごとのコールバック関数。 実行をスケジュールする、 *EvtInterruptDpc*コールバック関数、ドライバーを呼び出す必要があります[ **WdfInterruptQueueDpcForIsr** ](https://msdn.microsoft.com/library/windows/hardware/ff547371)内から、 [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数。

ドライバーが複数作成し場合[framework キュー オブジェクト](framework-queue-objects.md)デバイスごとに、別の使用を検討できます[DPC オブジェクト](https://msdn.microsoft.com/library/windows/hardware/dn265635)と[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)キューごとのコールバック関数。 実行をスケジュールする、 *EvtDpcFunc*コールバック関数を呼び出すことによって、ドライバーは 1 つまたは複数の DPC オブジェクトを作成する必要があります最初[ **WdfDpcCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547140)ドライバーの通常の[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 ドライバーの[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数を呼び出すことができます[ **WdfDpcEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff547148)します。

ドライバー通常[I/O 要求を完了](completing-i-o-requests.md)でその[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)コールバック関数。

ドライバーが IRQL で割り込みサービス操作を実行する必要がありますも = パッシブ\_レベル。 このような場合は、ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683) IRQL で実行中のコールバック関数ディスパッチ=\_レベル、1 つまたは複数の実行をスケジュールできます[フレームワークの作業項目](using-framework-work-items.md)の IRQL で実行 = パッシブ\_レベル。

デバイスの割り込みを処理中の作業項目を使用しているドライバーの例は、次を参照してください。、 [PCIDRV](sample-kmdf-drivers.md)サンプル ドライバー。

 

 





