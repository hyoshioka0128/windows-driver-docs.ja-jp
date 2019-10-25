---
title: 割り込みの移植
description: 割り込みの移植
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e90106be0a01fafe5832b70ea91db87b17ff5d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842250"
---
# <a name="porting-interrupts"></a>割り込みの移植


割り込みのサポートとサービスのためのコードは、WDF ドライバーと WDM ドライバーで似ています。 主な相違点が1つあります。

-   WDF ドライバーは、WDFINTERRUPT オブジェクトを作成し、その[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックから[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出すことによって、その割り込みサービスルーチン (ISR) コールバックを登録します。
-   WDM ドライバーは KINTERRUPT 構造体を作成し、IRP\_中に接続して[ **\_デバイス処理を開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)ます。

WDF ドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバックは、WDM ドライバーの[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンと同じタスクを実行します。 *EvtInterruptIsr* Callback は[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)を呼び出して、後でディスパッチ\_レベルで処理するために[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバックをキューに置いています。 応答として、フレームワークは、このコールバックを実行するシステムキューに DPC オブジェクトを追加します。

フレームワークの割り込みオブジェクトの詳細については、「[ハードウェア割り込みの処理](handling-hardware-interrupts.md)」を参照してください。

 

 





