---
Description: The User Mode Driver Framework (UMDF) requires that drivers support the IPnpCallback interface for Plug and Play (PnP) operations and the IPnpCallbackSelfManagedIo interface for power-management operations.
title: プラグ アンド プレイ (PnP) および電源管理をサポートしています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97331a23642518e39c10a218d19cdb1e85116bf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553965"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>プラグ アンド プレイ (PnP) および電源管理をサポートしています。


ユーザー モード ドライバー フレームワーク (UMDF) は、ドライバーがサポートする必要があります、 [ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)プラグ アンド プレイ (PnP) 操作のためのインターフェイスと[ **IPnpCallbackSelfManagedIo** ](https://msdn.microsoft.com/library/windows/hardware/ff556776)電源管理操作のためのインターフェイス。

最初のインターフェイス**IPnpCallback**プラグでは、ユーザーのときに呼び出されるメソッドをサポートまたはから切り離し、自分のデバイス。 2 番目のインターフェイス**IPnpCallbackSelfManagedIo**デバイスは、低電力状態にまたは、その稼働状態に戻ったときに呼び出されるメソッドをサポートしています。

WPD サンプルの 1 つを除くすべては、ハードウェアをエミュレートするため、これらのインターフェイス メソッドは意味のある作業を実行しないと、すぐに返します。

1 つの例外は、WpdBasicHardwareDriver サンプルです。 このドライバーは、実際のハードウェアをサポートするための 2 つの方法で動作するコードが含まれている、 **IPnpCallback**インターフェイス。 このサンプルでサポートされている 2 つのメソッドは[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)と[ **IPnpCallback::OnD0Exit**](https://msdn.microsoft.com/library/windows/hardware/ff556803)します。 最初のメソッドは、カーネル モードの RS232 ドライバーへの I/O 要求を転送するように、ドライバーのサンプルを使用する I/O ターゲットへのポインターを取得します。 このポインターを取得した後、 **IPnpCallback::OnDOEntry**メソッドは、I/O ターゲットを開始します。 2 番目のメソッドでは、 **IPnpCallback::OnD0Exit** I/O ターゲットへのポインターを取得し、それを停止します。

ドライバーは、ハードウェアをサポートする場合、またはこれらのインターフェイスの両方のサポートを追加します。 PnP の詳細な説明とユーザー モード デバイス ドライバーの電源管理では、[UMDF での PnP および電源管理のシナリオ](https://msdn.microsoft.com/library/windows/hardware/ff560452)を参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**IPnpCallback**](https://msdn.microsoft.com/library/windows/hardware/ff556762)

[**IPnpCallback::OnD0Entry**](https://msdn.microsoft.com/library/windows/hardware/ff556799)

[**IPnpCallback::OnD0Exit**](https://msdn.microsoft.com/library/windows/hardware/ff556803)

[**IPnpCallbackSelfManagedIo**](https://msdn.microsoft.com/library/windows/hardware/ff556776)

[UMDF PnP や電源管理のシナリオ](https://msdn.microsoft.com/library/windows/hardware/ff560452)

 

 





