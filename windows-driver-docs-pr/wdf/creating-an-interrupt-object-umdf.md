---
title: Interrupt オブジェクトの作成 (UMDF 1)
description: 割り込みオブジェクトの作成
ms.assetid: D281F2E8-3ADA-4F4E-B345-CE72FA3C69EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e738bdb4f1d9321c0e4847b833a23f54d51531
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141308"
---
# <a name="creating-an-interrupt-object-umdf-1"></a>Interrupt オブジェクトの作成 (UMDF 1)


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

デバイスのハードウェア割り込みを処理する UMDF ドライバーは、各デバイスがサポートできる各割り込みのフレームワーク割り込みオブジェクトを作成する必要があります。

通常、ドライバーは[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)にフレームワークの割り込みオブジェクトを作成します。 ただし、 [**IPnpCallbackHardware2:: On ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)に割り込みオブジェクトを作成することもできます。

フレームワークの割り込みオブジェクトを作成するには、ドライバーが[**Wudf の \_ 割り込み \_ 構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config)構造体を初期化し、それを[**IWDFDevice3:: createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)メソッドに渡す必要があります。 このメソッドは、ドライバーによって提供される次のイベントコールバック関数を登録します。

<a href="" id="oninterruptenable"></a>[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)  
ハードウェアの割り込みを有効にします。

<a href="" id="oninterruptdisable"></a>[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)  
ハードウェアの割り込みを無効にします。

<a href="" id="oninterruptisr"></a>[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)  
割り込みの割り込みサービスルーチン (ISR)。

<a href="" id="oninterruptworkitem"></a>[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)  
割り込みのワーカールーチン。

必要に応じて、ドライバーは[**Iwdfinterrupt:: SetPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-setpolicy)または[**Iwdfinterrupt:: SetExtendedPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-setextendedpolicy)を呼び出して、追加の割り込みパラメーターを指定できます。

このフレームワークは、ドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数を呼び出して、プラグアンドプレイ (PnP) マネージャーが割り込みベクターなどのシステムリソースをデバイスに割り当てます。 PnP マネージャーによってリソースが割り当てられると、そのデバイスの interrupt オブジェクトに割り込みリソースが格納されます。 (プラグアンドプレイをサポートしていないドライバーは、interrupt オブジェクトを使用できません)。

Windows Vista 以降のバージョンのオペレーティングシステムでは、メッセージシグナル割り込み (Msi) がサポートされています。 オペレーティングシステムがデバイスの Msi をサポートできるようにするには、ドライバーの INF ファイルでレジストリに値を設定する必要があります。 これらの値を設定する方法については、「[レジストリでのメッセージシグナル割り込みの有効化](https://docs.microsoft.com/windows-hardware/drivers/kernel/enabling-message-signaled-interrupts-in-the-registry)」を参照してください。

デバイスで特定の数の MSI メッセージがサポートされている場合、PnP マネージャーはその数のメッセージをデバイスに割り当てようとします。 PnP マネージャーが、デバイスがサポートできるすべてのメッセージを割り当てることができない場合、デバイスには1つのメッセージのみが割り当てられます。

ドライバーは、デバイスがサポートできる各割り込みベクターまたは MSI メッセージに対して、フレームワークの interrupt オブジェクトを作成する必要があります。 デバイスがサポートできるすべての割り込みリソースがデバイスに付与されていない場合、余分な割り込みオブジェクトは使用されず、コールバック関数は呼び出されません。

 

 





