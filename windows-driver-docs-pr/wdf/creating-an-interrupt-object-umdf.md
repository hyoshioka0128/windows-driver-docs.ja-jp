---
title: 割り込みオブジェクトを作成します。
description: 割り込みオブジェクトを作成します。
ms.assetid: D281F2E8-3ADA-4F4E-B345-CE72FA3C69EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5304ab2e648dfcaa0c39f8a764ab2e1a41de6842
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531599"
---
# <a name="creating-an-interrupt-object"></a>割り込みオブジェクトを作成します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスのハードウェアの割り込みを処理する UMDF ドライバーでは、各デバイスをサポートする各割り込みの framework 割り込みオブジェクトを作成する必要があります。

通常、ドライバー オブジェクトを作成します framework 割り込みで[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)します。 ただし、割り込みのオブジェクトの作成も[ **IPnpCallbackHardware2::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/hh439734)します。

フレームワークの割り込みオブジェクトを作成するには、ドライバーを初期化する必要があります、 [ **WUDF\_割り込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/hh464084)構造体に渡すと、 [ **IWDFDevice3::CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)メソッド。 このメソッドは、次のドライバーが指定したイベントのコールバック関数を登録します。

<a href="" id="oninterruptenable"></a>[*OnInterruptEnable*](https://msdn.microsoft.com/library/windows/hardware/hh463899)  
ハードウェアの割り込みを有効にします。

<a href="" id="oninterruptdisable"></a>[*OnInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/hh463895)  
ハードウェアの割り込みを無効にします。

<a href="" id="oninterruptisr"></a>[*OnInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/hh463902)  
割り込みの割り込みサービス ルーチン (ISR)。

<a href="" id="oninterruptworkitem"></a>[*OnInterruptWorkItem*](https://msdn.microsoft.com/library/windows/hardware/hh463905)  
割り込みのワーカーのルーチンです。

ドライバーを呼び出すことができます必要に応じて、 [ **IWDFInterrupt::SetPolicy** ](https://msdn.microsoft.com/library/windows/hardware/hh451328)または[ **IWDFInterrupt::SetExtendedPolicy** ](https://msdn.microsoft.com/library/windows/hardware/hh451324)追加を指定するにはパラメーターを中断します。

フレームワークは、ドライバーの[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)プラグ アンド プレイ (PnP) マネージャーがデバイスにベクトルの割り込みなどのシステム リソースを割り当てられる前に、コールバック関数。 後 PnP マネージャーでは、リソースを割り当てる、フレームワークには、割り込みのリソースがデバイスの割り込みのオブジェクトに格納します。 (プラグ アンド プレイをサポートしていないドライバーは、割り込みのオブジェクトを使用できません)

Windows Vista およびそれ以降のバージョンのオペレーティング システムでは、メッセージ シグナル割り込み (Msi) がサポートされています。 デバイスの Msi をサポートするために、オペレーティング システムを有効にするには、ドライバーの INF ファイルは、レジストリのいくつかの値を設定する必要があります。 これらの値を設定する方法については、[Enabling Message-Signaled がレジストリへの割り込み](https://msdn.microsoft.com/library/windows/hardware/ff544246)を参照してください。

デバイスは、MSI のメッセージ数をサポートできますが、PnP マネージャーはその数のメッセージをデバイスに割り当てるしようとします。 PnP マネージャーは、すべてのデバイスをサポートするメッセージを割り当てることはできない場合、は、1 つのメッセージをデバイスに割り当てます。

ドライバーは、割り込みベクトルまたはデバイスをサポートできる MSI メッセージごとに framework 割り込みオブジェクトを作成する必要があります。 PnP マネージャーは付与されないデバイスのすべてのデバイスをサポートする割り込みリソース、余分な割り込みオブジェクトを使用しませんし、これらのコールバック関数は呼び出されません。

 

 





