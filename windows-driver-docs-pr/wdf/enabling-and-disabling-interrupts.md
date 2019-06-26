---
title: 割り込みの有効化と無効化
description: 割り込みの有効化と無効化
ms.assetid: 432907e7-05a3-4a99-a291-33bd1eefa94c
keywords:
- ハードウェアの割り込み WDK KMDF、有効にします。
- 割り込み WDK KMDF、有効にします。
- ハードウェアの割り込み WDK KMDF、無効にします。
- 割り込み WDK KMDF、無効にします。
- 状態情報を有効にする、WDK KMDF を中断します。
- 状態情報を無効にする、WDK KMDF を中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57da85c8607baf9f0fd429f1f13c552a8456d0e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368728"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


ドライバーは、デバイスの割り込みを処理する場合は指定する必要があります[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)と[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック有効にして、割り込みを無効にする機能です。 通常、これらのコールバック関数は、デバイスの DIRQL に実行され、有効にして、デバイスの割り込みメカニズムを無効にするのに必要なことすべてを行う必要があります。 [パッシブ レベルの割り込み](supporting-passive-level-interrupts.md)IRQL でこれらのコールバック関数の実行、割り込みのパッシブ レベルのロックを押しながら PASSIVE_LEVEL を =。

IRQL でこれらの追加の操作を実行できない場合、ドライバーが有効化または割り込みを無効化に関連する追加の操作を実行する場合と = DIRQL、ドライバーを指定できますも[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)と[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数。 これら 2 つのコールバック関数は IRQL で実行 = パッシブ\_割り込みロックなしでレベルが保持されているし、フレームワークには IRQL で利用できないオブジェクトのメソッドを呼び出すことができます = DIRQL します。

フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)と[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数毎回デバイス状態にその作業 (D0)、フレームワークには、ドライバーが呼び出された後[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数。

フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)と[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数フレームワークは、ドライバーの前に、デバイスが、作業の状態を離れるたび[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数。 詳細については、フレームワークがドライバーのコールバック関数を呼び出すと、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

あるデバイスが同じリソースを使用割り込みたびに、フレームワーク、ドライバーを想定する必要があります[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)コールバック関数。 PnP マネージャーも[システム リソースを再分配します](the-pnp-manager-redistributes-system-resources.md)、し、デバイスに割り込みの新しいリソースに割り当てることができます。

ドライバーを呼び出すことができます[ **WdfInterruptGetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetinfo)デバイスの割り込みのリソースが決定します。 ドライバーを呼び出すことができます[ **WdfInterruptGetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetdevice)割り込みオブジェクトが属しているデバイスを決定します。 (いくつかのドライバーが呼び出す可能性があります[ **WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt))。

ドライバーを有効にするを直接割り込みを無効にするには、割り込みオブジェクトを呼び出すことができます[ **WdfInterruptEnable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)と[ **WdfInterruptDisable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)メソッドを呼び出してドライバーの[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)と[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)イベントコールバック関数。 ただし、ほとんどのドライバーがようにするだけでを呼び出すために、フレームワーク、 *EvtInterruptEnable*と*EvtInterruptDisable*適切なタイミングでコールバック関数。

 

 





