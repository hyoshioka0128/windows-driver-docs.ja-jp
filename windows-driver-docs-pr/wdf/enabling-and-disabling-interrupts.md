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
ms.openlocfilehash: cfb5e9d1f02c7f6d68cf8cc4c52927dc82840244
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571137"
---
# <a name="enabling-and-disabling-interrupts"></a>割り込みの有効化と無効化


ドライバーは、デバイスの割り込みを処理する場合は指定する必要があります[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)と[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック有効にして、割り込みを無効にする機能です。 通常、これらのコールバック関数は、デバイスの DIRQL に実行され、有効にして、デバイスの割り込みメカニズムを無効にするのに必要なことすべてを行う必要があります。 [パッシブ レベルの割り込み](supporting-passive-level-interrupts.md)IRQL でこれらのコールバック関数の実行、割り込みのパッシブ レベルのロックを押しながら PASSIVE_LEVEL を =。

IRQL でこれらの追加の操作を実行できない場合、ドライバーが有効化または割り込みを無効化に関連する追加の操作を実行する場合と = DIRQL、ドライバーを指定できますも[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)と[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)コールバック関数。 これら 2 つのコールバック関数は IRQL で実行 = パッシブ\_割り込みロックなしでレベルが保持されているし、フレームワークには IRQL で利用できないオブジェクトのメソッドを呼び出すことができます = DIRQL します。

フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)と[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)コールバック関数毎回デバイス状態にその作業 (D0)、フレームワークには、ドライバーが呼び出された後[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数。

フレームワークは、ドライバーの[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)と[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)コールバック関数フレームワークは、ドライバーの前に、デバイスが、作業の状態を離れるたび[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック関数。 詳細については、フレームワークがドライバーのコールバック関数を呼び出すと、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

あるデバイスが同じリソースを使用割り込みたびに、フレームワーク、ドライバーを想定する必要があります[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)コールバック関数。 PnP マネージャーも[システム リソースを再分配します](the-pnp-manager-redistributes-system-resources.md)、し、デバイスに割り込みの新しいリソースに割り当てることができます。

ドライバーを呼び出すことができます[ **WdfInterruptGetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547367)デバイスの割り込みのリソースが決定します。 ドライバーを呼び出すことができます[ **WdfInterruptGetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff547358)割り込みオブジェクトが属しているデバイスを決定します。 (いくつかのドライバーが呼び出す可能性があります[ **WdfInterruptWdmGetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff547393))。

ドライバーを有効にするを直接割り込みを無効にするには、割り込みオブジェクトを呼び出すことができます[ **WdfInterruptEnable** ](https://msdn.microsoft.com/library/windows/hardware/ff547354)と[ **WdfInterruptDisable** ](https://msdn.microsoft.com/library/windows/hardware/ff547351)メソッドを呼び出してドライバーの[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)と[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)イベントコールバック関数。 ただし、ほとんどのドライバーがようにするだけでを呼び出すために、フレームワーク、 *EvtInterruptEnable*と*EvtInterruptDisable*適切なタイミングでコールバック関数。

 

 





