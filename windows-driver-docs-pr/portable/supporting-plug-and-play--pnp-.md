---
Description: ユーザー モード ドライバー フレームワーク (UMDF) では、ドライバーが、電源管理操作のために、プラグ アンド プレイ (PnP) 操作の IPnpCallback インターフェイスと IPnpCallbackSelfManagedIo インターフェイスをサポートすることが必要です。
title: プラグ アンド プレイ (PnP) と電源管理のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13508feaaf868bca8aeb08324511ce4555b3dc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387179"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>プラグ アンド プレイ (PnP) と電源管理のサポート


ユーザー モード ドライバー フレームワーク (UMDF) は、ドライバーがサポートする必要があります、 [ **IPnpCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)プラグ アンド プレイ (PnP) 操作のためのインターフェイスと[ **IPnpCallbackSelfManagedIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)電源管理操作のためのインターフェイス。

最初のインターフェイス**IPnpCallback**プラグでは、ユーザーのときに呼び出されるメソッドをサポートまたはから切り離し、自分のデバイス。 2 番目のインターフェイス**IPnpCallbackSelfManagedIo**デバイスは、低電力状態にまたは、その稼働状態に戻ったときに呼び出されるメソッドをサポートしています。

WPD サンプルの 1 つを除くすべては、ハードウェアをエミュレートするため、これらのインターフェイス メソッドは意味のある作業を実行しないと、すぐに返します。

1 つの例外は、WpdBasicHardwareDriver サンプルです。 このドライバーは、実際のハードウェアをサポートするための 2 つの方法で動作するコードが含まれている、 **IPnpCallback**インターフェイス。 このサンプルでサポートされている 2 つのメソッドは[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)と[ **IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)します。 最初のメソッドは、カーネル モードの RS232 ドライバーへの I/O 要求を転送するように、ドライバーのサンプルを使用する I/O ターゲットへのポインターを取得します。 このポインターを取得した後、 **IPnpCallback::OnDOEntry**メソッドは、I/O ターゲットを開始します。 2 番目のメソッドでは、 **IPnpCallback::OnD0Exit** I/O ターゲットへのポインターを取得し、それを停止します。

ドライバーは、ハードウェアをサポートする場合、またはこれらのインターフェイスの両方のサポートを追加します。 PnP の詳細な説明とユーザー モード デバイス ドライバーの電源管理では、次を参照してください。 [UMDF での PnP および電源管理のシナリオ](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallback::OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)

[**IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[UMDF PnP や電源管理のシナリオ](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)

 

 





