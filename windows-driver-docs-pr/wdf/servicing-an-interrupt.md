---
title: 割り込みの処理
description: 割り込みの処理
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
ms.openlocfilehash: 1c265a458ca8a852b67fd4452c86f25a23fa3963
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376188"
---
# <a name="servicing-an-interrupt"></a>割り込みの処理


このトピックでは、DIRQL 割り込みを処理する方法を説明します。 パッシブ レベル割り込みを処理する方法の詳細については、次を参照してください。[パッシブ レベルをサポートしている中断](supporting-passive-level-interrupts.md#servicing)します。

割り込みをサービスは、2 つ、および場合によって 3 つの手順で構成されます。

1.  レジスタの内容) などの揮発性の情報を迅速に保存するには、IRQL で実行される割り込みサービス ルーチン = DIRQL います。

2.  IRQL で実行される遅延プロシージャ呼び出し (DPC) の保存された揮発性の情報を処理するディスパッチ =\_レベル。

3.  追加の作業を実行する IRQL = パッシブ\_レベルに必要な場合。

どのフレームワーク ベースのドライバーの実装として、ドライバーの割り込みサービス ルーチン (ISR) フレームワークをデバイスでは、ハードウェア割り込みを生成するとき、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数。

[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)などレジスタの内容、もう 1 つの割り込みが発生した場合に失われますが、デバイスの DIRQL、割り込みについては、簡単に保存する必要がありますで実行されるコールバック関数。

通常、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数が低いかどうかを後で保存された情報の処理に遅延プロシージャ呼び出し (DPC) をスケジュール (ディスパッチ\_レベル)。 フレームワーク ベースのドライバーと DPC ルーチンを実装する[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数。

ほとんどのドライバーを使用して、1 つ[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)割り込みの種類ごとのコールバック関数。 実行をスケジュールする、 *EvtInterruptDpc*コールバック関数、ドライバーを呼び出す必要があります[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)内から、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数。

ドライバーが複数作成し場合[framework キュー オブジェクト](framework-queue-objects.md)デバイスごとに、別の使用を検討できます[DPC オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/)と[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)キューごとのコールバック関数。 実行をスケジュールする、 *EvtDpcFunc*コールバック関数を呼び出すことによって、ドライバーは 1 つまたは複数の DPC オブジェクトを作成する必要があります最初[ **WdfDpcCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpccreate)ドライバーの通常の[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。 ドライバーの[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数を呼び出すことができます[ **WdfDpcEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcenqueue)します。

ドライバー通常[I/O 要求を完了](completing-i-o-requests.md)でその[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数。

ドライバーが IRQL で割り込みサービス操作を実行する必要がありますも = パッシブ\_レベル。 このような場合は、ドライバーの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc) IRQL で実行中のコールバック関数ディスパッチ=\_レベル、1 つまたは複数の実行をスケジュールできます[フレームワークの作業項目](using-framework-work-items.md)の IRQL で実行 = パッシブ\_レベル。

デバイスの割り込みを処理中の作業項目を使用しているドライバーの例は、次を参照してください。、 [PCIDRV](sample-kmdf-drivers.md)サンプル ドライバー。

 

 





