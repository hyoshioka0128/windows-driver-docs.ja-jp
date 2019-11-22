---
title: 割り込みの有効化と無効化
description: 割り込みの有効化と無効化
ms.assetid: 432907e7-05a3-4a99-a291-33bd1eefa94c
keywords:
- ハードウェア割り込み WDK KMDF、有効化
- WDK KMDF を中断し、を有効にします。
- ハードウェア割り込み WDK KMDF、無効化
- WDK KMDF を中断し、無効にします。
- 状態情報 WDK KMDF、割り込みの有効化
- 状態情報 WDK KMDF、割り込みの無効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6267a435b4d1ea55a5ac9ddc5867e3b42cbaad03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843191"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


ドライバーがデバイスの割り込みを処理する場合は、割り込みを有効または無効にする[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)および[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数を提供する必要があります。 通常、これらのコールバック関数はデバイスの DIRQL で実行され、デバイスの割り込みメカニズムを有効または無効にするために必要な操作を行う必要があります。 [パッシブレベルの割り込み](supporting-passive-level-interrupts.md)の場合、これらのコールバック関数は、パッシブレベルの割り込みロックを保持した状態で、IRQL = PASSIVE_LEVEL で実行されます。

ドライバーで割り込みの有効化または無効化に関連する追加の操作を実行する必要があり、これらの追加操作を IRQL = DIRQL で実行できない場合、ドライバーは[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)とを[*提供することもできます。EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数。 これら2つのコールバック関数は、割り込みロックを保持せずに IRQL = パッシブ\_レベルで実行され、IRQL = DIRQL で使用できないフレームワークオブジェクトメソッドを呼び出すことができます。

フレームワークは、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) callback 関数を呼び出した後に、デバイスが動作 (D0) 状態になるたびに、ドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)コールバック関数と[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数を呼び出します。

フレームワークは、ドライバーの[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)を呼び出す前に、デバイスが動作状態のままになるたびに、ドライバーの[*EvtDeviceD0ExitPreInterruptsDisabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)コールバック関数と[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)コールバック関数を呼び出します。コールバック関数。 フレームワークがドライバーのコールバック関数を呼び出すタイミングの詳細については、「 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)」を参照してください。

フレームワークがドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) callback 関数を呼び出すたびに、デバイスで同じ割り込みリソースが使用されると想定しないでください。 PnP マネージャによって[システムリソース](the-pnp-manager-redistributes-system-resources.md)が再配布される場合があり、デバイスに新しい割り込みリソースが割り当てられることがあります。

ドライバーは[**WdfInterruptGetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetinfo)を呼び出して、デバイスの割り込みリソースを特定できます。 ドライバーは、 [**WdfInterruptGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetdevice)を呼び出して、割り込みオブジェクトが属しているデバイスを特定できます。 (一部のドライバーは[**WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)を呼び出す可能性があります)。

割り込みを直接有効または無効にするために、ドライバーは、ドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)および[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)イベントを呼び出す interrupt オブジェクトの[**WdfInterruptEnable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)メソッドと[**WdfInterruptDisable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)メソッドを呼び出すことができます。コールバック関数。 ただし、ほとんどのドライバーは、適切なタイミングで*EvtInterruptEnable*および*EvtInterruptDisable*コールバック関数を呼び出すことをフレームワークに許可するだけです。

 

 





