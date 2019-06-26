---
title: 割り込みの移植
description: 割り込みの移植
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae585ccb665feea1d245439cb31ac7f7c32bfb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379634"
---
# <a name="porting-interrupts"></a>割り込みの移植


サポートしていると、割り込みのコードは、WDF と WDM ドライバーと似ています。 1 つの主な違いがあります。

-   WDF ドライバー WDFINTERRUPT オブジェクトを作成し、呼び出すことによって、割り込みサービス ルーチン (ISR) のコールバックを登録します[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)からその[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック。
-   WDM ドライバーが KINTERRUPT 構造を作成し、接続中に[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)処理します。

[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) WDF ドライバーでのコールバック WDM ドライバーのと同じタスクを実行する[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)ルーチン。 *EvtInterruptIsr*コールバック呼び出し[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)キューに、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)ディスパッチに後で処理するためのコールバック\_レベル。 応答では、フレームワークは、このコールバックを実行しているシステム キューに DPC オブジェクトを追加します。

フレームワークの割り込みのオブジェクトの詳細については、次を参照してください。[ハードウェアの割り込み処理](handling-hardware-interrupts.md)します。

 

 





