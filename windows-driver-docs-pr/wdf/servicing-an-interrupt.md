---
title: 割り込みの処理
description: 割り込みの処理
ms.assetid: b6306d2c-a7be-4fc3-8123-4d2b5c60c988
keywords:
- ハードウェア割り込み WDK KMDF、サービス
- WDK KMDF、サービスを中断します。
- サービスの割り込み (WDK KMDF)
- 割り込みサービスルーチン WDK KMDF
- Isr WDK KMDF
- 遅延プロシージャ呼び出し WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76aa653a7eac3b04416f20822fc0c1f86593ef8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842192"
---
# <a name="servicing-an-interrupt"></a>割り込みの処理


このトピックでは、DIRQL 割り込みを処理する方法について説明します。 パッシブレベルの割り込みのサービスの詳細については、「[パッシブレベルの割り込みのサポート](supporting-passive-level-interrupts.md#servicing)」を参照してください。

割り込みのサービスは、次の2つの手順で構成されます。

1.  IRQL = DIRQL で実行される割り込みサービスルーチンで、揮発性情報 (レジスタの内容など) をすばやく保存する。

2.  IRQL = ディスパッチ\_レベルで実行される遅延プロシージャ呼び出し (DPC) で、保存されている volatile 情報を処理します。

3.  必要に応じて、IRQL = パッシブ\_レベルで追加の作業を実行します。

デバイスがハードウェア割り込みを生成すると、フレームワークは、ドライバーの interrupt service ルーチン (ISR) を呼び出します。これは、フレームワークベースのドライバーが[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数として実装します。

デバイスの DIRQL で実行される[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、別の割り込みが発生した場合に失われる、レジスタの内容などの割り込み情報をすばやく保存する必要があります。

通常、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、遅延プロシージャ呼び出し (DPC) をスケジュールして、保存された情報を後で低い IRQL (ディスパッチ\_レベル) で処理するようにスケジュールします。 フレームワークベースのドライバーは、DPC ルーチンを[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) callback 関数として実装します。

ほとんどのドライバーでは、割り込みの種類ごとに1つの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数を使用します。 *EvtInterruptDpc* callback 関数の実行をスケジュールするには、ドライバーが[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) Callback 関数内から[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)を呼び出す必要があります。

ドライバーが各デバイスに対して複数の[フレームワークキューオブジェクト](framework-queue-objects.md)を作成する場合は、キューごとに個別の[DPC オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/)と[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数を使用することを検討してください。 *EvtDpcFunc*コールバック関数の実行をスケジュールするには、ドライバーが[**WdfDpcCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpccreate)を呼び出すことによって、最初に1つ以上の DPC オブジェクトを作成する必要があります。通常は、ドライバーの[*evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出します。 次に、ドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、 [**Wdfdpcenqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)を呼び出すことができます。

ドライバーは通常、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数で[i/o 要求を完了](completing-i-o-requests.md)します。

場合によっては、ドライバーで一部の割り込みサービス操作を IRQL = パッシブ\_レベルで実行する必要があります。 このような場合、IRQL = ディスパッチ\_レベルで実行されるドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数は、IRQL = パッシブ\_レベルで実行される1つ以上の[フレームワーク作業項目](using-framework-work-items.md)の実行をスケジュールできます。

デバイス割り込みの処理中に作業項目を使用するドライバーの例については、 [Pcidrv](sample-kmdf-drivers.md)サンプルドライバーを参照してください。

 

 





