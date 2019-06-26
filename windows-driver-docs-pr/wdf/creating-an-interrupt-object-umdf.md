---
title: 割り込みオブジェクトの作成
description: 割り込みオブジェクトの作成
ms.assetid: D281F2E8-3ADA-4F4E-B345-CE72FA3C69EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7442cbcafec322027c0c82acb43a985500f2638f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382421"
---
# <a name="creating-an-interrupt-object"></a>割り込みオブジェクトの作成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスのハードウェアの割り込みを処理する UMDF ドライバーでは、各デバイスをサポートする各割り込みの framework 割り込みオブジェクトを作成する必要があります。

通常、ドライバー オブジェクトを作成します framework 割り込みで[ **IDriverEntry::OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)します。 ただし、割り込みのオブジェクトの作成も[ **IPnpCallbackHardware2::OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)します。

フレームワークの割り込みオブジェクトを作成するには、ドライバーを初期化する必要があります、 [ **WUDF\_割り込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config)構造体に渡すと、 [ **IWDFDevice3::CreateInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)メソッド。 このメソッドは、次のドライバーが指定したイベントのコールバック関数を登録します。

<a href="" id="oninterruptenable"></a>[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)  
ハードウェアの割り込みを有効にします。

<a href="" id="oninterruptdisable"></a>[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)  
ハードウェアの割り込みを無効にします。

<a href="" id="oninterruptisr"></a>[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)  
割り込みの割り込みサービス ルーチン (ISR)。

<a href="" id="oninterruptworkitem"></a>[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)  
割り込みのワーカーのルーチンです。

ドライバーを呼び出すことができます必要に応じて、 [ **IWDFInterrupt::SetPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-setpolicy)または[ **IWDFInterrupt::SetExtendedPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-setextendedpolicy)追加を指定するにはパラメーターを中断します。

フレームワークは、ドライバーの[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)プラグ アンド プレイ (PnP) マネージャーがデバイスにベクトルの割り込みなどのシステム リソースを割り当てられる前に、コールバック関数。 後 PnP マネージャーでは、リソースを割り当てる、フレームワークには、割り込みのリソースがデバイスの割り込みのオブジェクトに格納します。 (プラグ アンド プレイをサポートしていないドライバーは、割り込みのオブジェクトを使用できません)

Windows Vista およびそれ以降のバージョンのオペレーティング システムでは、メッセージ シグナル割り込み (Msi) がサポートされています。 デバイスの Msi をサポートするために、オペレーティング システムを有効にするには、ドライバーの INF ファイルは、レジストリのいくつかの値を設定する必要があります。 これらの値を設定する方法については、次を参照してください。 [Enabling Message-Signaled がレジストリへの割り込み](https://docs.microsoft.com/windows-hardware/drivers/kernel/enabling-message-signaled-interrupts-in-the-registry)します。

デバイスは、MSI のメッセージ数をサポートできますが、PnP マネージャーはその数のメッセージをデバイスに割り当てるしようとします。 PnP マネージャーは、すべてのデバイスをサポートするメッセージを割り当てることはできない場合、は、1 つのメッセージをデバイスに割り当てます。

ドライバーは、割り込みベクトルまたはデバイスをサポートできる MSI メッセージごとに framework 割り込みオブジェクトを作成する必要があります。 PnP マネージャーは付与されないデバイスのすべてのデバイスをサポートする割り込みリソース、余分な割り込みオブジェクトを使用しませんし、これらのコールバック関数は呼び出されません。

 

 





