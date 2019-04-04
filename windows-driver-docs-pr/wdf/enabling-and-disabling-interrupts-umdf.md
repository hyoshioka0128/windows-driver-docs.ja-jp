---
title: 割り込みの有効化と無効化
description: 割り込みの有効化と無効化
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02834e52849b93c4f9cbb0c2966d4c69321e6ab2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577696"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、デバイスの割り込みを処理する場合は指定する必要があります[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)と[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)コールバック関数有効にし、割り込みを無効にします。 これらのコールバック関数では、有効にして、デバイスの割り込みメカニズムを無効にするのに必要なことすべてを行う必要があります。

場合は、ドライバーが有効にしたり、ドライバーを指定できますも、割り込みを無効にすると関連するその他の操作を実行する必要があります[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439750)と[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439755)コールバック関数。

フレームワークは、ドライバーの[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)と[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439750)コールバック関数、デバイスがその作業 (D0) を入力するたびに状態では、フレームワークには、ドライバーが呼び出された後[ **OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)コールバック関数。 フレームワークは、ドライバーの[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439755)と[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)コールバック関数、フレームワーク、ドライバーの前に、デバイスが、作業の状態を離れるたび[ **OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)コールバック関数。 詳細については、フレームワークがドライバーのコールバック関数を呼び出すと、[UMDF ベースのドライバーでの PnP と電源管理](pnp-and-power-management-in-umdf-drivers.md)を参照してください。

あるデバイスが同じリソースを使用割り込みたびに、フレームワーク、ドライバーを想定する必要があります[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)コールバック関数。 PnP マネージャーが、システム リソースを分配することもありますし、デバイスに新しい割り込みリソースを割り当てることができます、します。

ドライバーを呼び出すことができます[ **IWDFInterrupt::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451309)デバイスの割り込みのリソースが決定します。 ドライバーを呼び出すことができます[ **IWDFInterrupt::GetDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh451305)割り込みオブジェクトが属しているデバイスを決定します。

ドライバーを有効にするを直接割り込みを無効にするには、割り込みオブジェクトを呼び出すことができます[ **IWDFInterrupt::Enable** ](https://msdn.microsoft.com/library/windows/hardware/hh451300)と[ **IWDFInterrupt::Disable**](https://msdn.microsoft.com/library/windows/hardware/hh451295)メソッドを呼び出してドライバーの[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)と[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)イベントコールバック関数。 ただし、ほとんどのドライバーがようにするだけでを呼び出すために、フレームワーク、 *OnInterruptEnable*と*OnInterruptDisable*適切なタイミングでコールバック関数。

 

 





