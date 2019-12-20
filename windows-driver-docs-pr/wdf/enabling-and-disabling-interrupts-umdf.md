---
title: 割り込みの有効化と無効化
description: 割り込みの有効化と無効化
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c86d5948c4c6f0b162d415fe790177ebc3585e74
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210460"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーがデバイスの割り込みを処理する場合は、割り込みを有効または無効にする[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)および[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)コールバック関数を提供する必要があります。 これらのコールバック関数は、デバイスの割り込みメカニズムを有効または無効にするために必要な操作を行う必要があります。

ドライバーで割り込みの有効化または無効化に関連する追加の操作を実行する必要がある場合は、ドライバーで[**IPnpCallbackHardwareInterrupt:: OnD0EntryPostInterruptsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)および[**IPnpCallbackHardwareInterrupt:: OnD0ExitPreInterruptsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled) callback 関数を指定することもできます。

フレームワークは、ドライバーの[**OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) callback 関数を呼び出した後に、デバイスが動作 (D0) 状態になるたびに、ドライバーの[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)および[**IPnpCallbackHardwareInterrupt:: OnD0EntryPostInterruptsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled) callback 関数を呼び出します。 フレームワークは、ドライバーの[**OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) callback 関数を呼び出す前に、デバイスが動作状態のままになるたびに、ドライバーの[**IPnpCallbackHardwareInterrupt:: OnD0ExitPreInterruptsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)関数と[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable) callback 関数を呼び出します。 フレームワークがドライバーのコールバック関数を呼び出すタイミングの詳細については、「 [UMDF ベースのドライバーの PnP および電源管理](pnp-and-power-management-in-umdf-drivers.md)」を参照してください。

フレームワークがドライバーの[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable) callback 関数を呼び出すたびに、デバイスで同じ割り込みリソースが使用されると想定しないでください。 PnP マネージャによってシステムリソースが再配布される場合があり、デバイスに新しい割り込みリソースが割り当てられることがあります。

ドライバーは[**Iwdfinterrupt:: GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getinfo)を呼び出して、デバイスの割り込みリソースを特定できます。 ドライバーは、 [**Iwdfinterrupt:: GetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getdevice)を呼び出して、割り込みオブジェクトが属しているデバイスを特定できます。

割り込みを直接有効または無効にするために、ドライバーは、interrupt オブジェクトの[**Iwdfinterrupt:: enable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-enable)メソッドと[**iwdfinterrupt::D**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-disable)無効にするメソッドを呼び出すことができます。このメソッドは、ドライバーの[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)および[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)イベントコールバック関数を呼び出します。 ただし、ほとんどのドライバーは、適切なタイミングで*OnInterruptEnable*および*OnInterruptDisable*コールバック関数を呼び出すことをフレームワークに許可するだけです。

 

 





