---
title: 割り込みの有効化と無効化
description: 割り込みの有効化と無効化
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe10c29c925970fb2efe36ef709229d7f164ae0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368734"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、デバイスの割り込みを処理する場合は指定する必要があります[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)と[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)コールバック関数有効にし、割り込みを無効にします。 これらのコールバック関数では、有効にして、デバイスの割り込みメカニズムを無効にするのに必要なことすべてを行う必要があります。

場合は、ドライバーが有効にしたり、ドライバーを指定できますも、割り込みを無効にすると関連するその他の操作を実行する必要があります[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)と[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)コールバック関数。

フレームワークは、ドライバーの[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)と[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)コールバック関数、デバイスがその作業 (D0) を入力するたびに状態では、フレームワークには、ドライバーが呼び出された後[ **OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)コールバック関数。 フレームワークは、ドライバーの[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)と[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)コールバック関数、フレームワーク、ドライバーの前に、デバイスが、作業の状態を離れるたび[ **OnD0Exit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)コールバック関数。 詳細については、フレームワークがドライバーのコールバック関数を呼び出すと、次を参照してください。 [UMDF ベースのドライバーでの PnP と電源管理](pnp-and-power-management-in-umdf-drivers.md)します。

あるデバイスが同じリソースを使用割り込みたびに、フレームワーク、ドライバーを想定する必要があります[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)コールバック関数。 PnP マネージャーが、システム リソースを分配することもありますし、デバイスに新しい割り込みリソースを割り当てることができます、します。

ドライバーを呼び出すことができます[ **IWDFInterrupt::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-getinfo)デバイスの割り込みのリソースが決定します。 ドライバーを呼び出すことができます[ **IWDFInterrupt::GetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-getdevice)割り込みオブジェクトが属しているデバイスを決定します。

ドライバーを有効にするを直接割り込みを無効にするには、割り込みオブジェクトを呼び出すことができます[ **IWDFInterrupt::Enable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-enable)と[ **IWDFInterrupt::Disable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-disable)メソッドを呼び出してドライバーの[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)と[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)イベントコールバック関数。 ただし、ほとんどのドライバーがようにするだけでを呼び出すために、フレームワーク、 *OnInterruptEnable*と*OnInterruptDisable*適切なタイミングでコールバック関数。

 

 





