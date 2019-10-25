---
Description: ユーザーモードドライバーフレームワーク (UMDF) では、ドライバーがプラグアンドプレイ (PnP) 操作用の IPnpCallback インターフェイス、および電源管理操作用の IPnpCallbackSelfManagedIo インターフェイスをサポートしている必要があります。
title: プラグ アンド プレイ (PnP) と電源管理のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0e0a4c0ca4dc3e6e83dbda69109291ee5cccf95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843579"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>プラグ アンド プレイ (PnP) と電源管理のサポート


ユーザーモードドライバーフレームワーク (UMDF) では、ドライバーがプラグアンドプレイ (PnP) 操作用の[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)インターフェイス、および電源管理操作用の[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)インターフェイスをサポートしている必要があります。

1つ目のインターフェイスである**IPnpCallback**は、ユーザーがデバイスをプラグインまたは unplugs するときに呼び出されるメソッドをサポートしています。 2番目のインターフェイス**IPnpCallbackSelfManagedIo**は、デバイスが低電力状態になったときに呼び出されるメソッドをサポートします。または、が動作状態に戻ります。

1つを除くすべての WPD サンプルはハードウェアをエミュレートするため、これらのインターフェイスのメソッドは意味のある処理を行わず、すぐに制御を戻します。

1つの例外は、Wpdbasicハードウェアドライバーサンプルです。 このドライバーは実際のハードウェアをサポートしているため、 **IPnpCallback**インターフェイスの2つのメソッドの作業コードが含まれています。 このサンプルでサポートされている2つの方法は、 [**IPnpCallback:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)と[**IPnpCallback:: OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)です。 最初のメソッドは、カーネルモードの RS232 ドライバーに i/o 要求を転送するためにサンプルドライバーが使用する i/o ターゲットへのポインターを取得します。 このポインターを取得すると、 **IPnpCallback:: OnDOEntry**メソッドによって i/o ターゲットが開始されます。 2番目のメソッド**IPnpCallback:: OnD0Exit**は、i/o ターゲットへのポインターを取得し、それを停止します。

ドライバーがハードウェアをサポートしている場合は、これらのインターフェイスのいずれかまたは両方のサポートを追加することをお勧めします。 ユーザーモードのデバイスドライバーでの PnP と電源管理の詳細については、「 [UMDF の pnp および電源管理のシナリオ](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallback::OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)

[**IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[UMDF の PnP および電源管理のシナリオ](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)

 

 





