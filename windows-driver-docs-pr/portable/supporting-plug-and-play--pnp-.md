---
Description: ユーザー モード ドライバー フレームワーク (UMDF) では、ドライバーが、電源管理操作のために、プラグ アンド プレイ (PnP) 操作の IPnpCallback インターフェイスと IPnpCallbackSelfManagedIo インターフェイスをサポートすることが必要です。
title: プラグ アンド プレイ (PnP) と電源管理のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97331a23642518e39c10a218d19cdb1e85116bf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380855"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>プラグ アンド プレイ (PnP) と電源管理のサポート


ユーザー モード ドライバー フレームワーク (UMDF) は、ドライバーがサポートする必要があります、 [ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)プラグ アンド プレイ (PnP) 操作のためのインターフェイスと[ **IPnpCallbackSelfManagedIo** ](https://msdn.microsoft.com/library/windows/hardware/ff556776)電源管理操作のためのインターフェイス。

最初のインターフェイス**IPnpCallback**プラグでは、ユーザーのときに呼び出されるメソッドをサポートまたはから切り離し、自分のデバイス。 2 番目のインターフェイス**IPnpCallbackSelfManagedIo**デバイスは、低電力状態にまたは、その稼働状態に戻ったときに呼び出されるメソッドをサポートしています。

WPD サンプルの 1 つを除くすべては、ハードウェアをエミュレートするため、これらのインターフェイス メソッドは意味のある作業を実行しないと、すぐに返します。

1 つの例外は、WpdBasicHardwareDriver サンプルです。 このドライバーは、実際のハードウェアをサポートするための 2 つの方法で動作するコードが含まれている、 **IPnpCallback**インターフェイス。 このサンプルでサポートされている 2 つのメソッドは[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)と[ **IPnpCallback::OnD0Exit**](https://msdn.microsoft.com/library/windows/hardware/ff556803)します。 最初のメソッドは、カーネル モードの RS232 ドライバーへの I/O 要求を転送するように、ドライバーのサンプルを使用する I/O ターゲットへのポインターを取得します。 このポインターを取得した後、 **IPnpCallback::OnDOEntry**メソッドは、I/O ターゲットを開始します。 2 番目のメソッドでは、 **IPnpCallback::OnD0Exit** I/O ターゲットへのポインターを取得し、それを停止します。

ドライバーは、ハードウェアをサポートする場合、またはこれらのインターフェイスの両方のサポートを追加します。 PnP の詳細な説明とユーザー モード デバイス ドライバーの電源管理では、次を参照してください。 [UMDF での PnP および電源管理のシナリオ](https://msdn.microsoft.com/library/windows/hardware/ff560452)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**IPnpCallback**](https://msdn.microsoft.com/library/windows/hardware/ff556762)

[**IPnpCallback::OnD0Entry**](https://msdn.microsoft.com/library/windows/hardware/ff556799)

[**IPnpCallback::OnD0Exit**](https://msdn.microsoft.com/library/windows/hardware/ff556803)

[**IPnpCallbackSelfManagedIo**](https://msdn.microsoft.com/library/windows/hardware/ff556776)

[UMDF PnP や電源管理のシナリオ](https://msdn.microsoft.com/library/windows/hardware/ff560452)

 

 





