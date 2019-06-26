---
title: AVStream のクロック
description: AVStream のクロック
ms.assetid: fc1d5bca-72e3-48e2-b46f-09a13bba83b4
keywords:
- WDK AVStream をクロックします。
- AVStream クロック WDK
- WDK AVStream のクロックをピン留め
- WDK AVStream のタイマー
- WDK AVStream の時間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef24bd850ce2eb63f5935e8da7de7c416c224b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386710"
---
# <a name="avstream-clocks"></a>AVStream のクロック





AVStream のフィルターでは、pin でのクロックがサポートされます。

で、AVStream 暗証番号 (pin) が時計を公開していることを示す設定 KSPIN\_フラグ\_実装\_出勤、**フラグ**最初のメンバー [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)で、 **PinDescriptors**のメンバー [ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor).

ポインターを提供する[ **KSCLOCK\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksclock_dispatch)構造体[ **KSPIN\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)します。

クロックの要求で定義されたメソッドを使用して、 [IKsReferenceClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-iksreferenceclock)インターフェイス。 取得することができます、 *IKsReferenceClock*呼び出してインターフェイス[ **KsPinGetReferenceClockInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetreferenceclockinterface)します。 AVStream ミニドライバーが完了すると、インターフェイスを解放します。

配置するタイマー値を取得する、 **PresentationTime**フィールド[ **KSSTREAM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)、呼び出す[ **IKsReferenceClock::GetCorrelatedTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-iksreferenceclock-getcorrelatedtime)します。

クロックが選択されている場合でも、クロックが決して GraphEdit に表示されることに注意してください。

クロックが選択されていることを確認するへの呼び出しを確認します。 [IKsReferenceClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-iksreferenceclock)メソッド KSCLOCK で指定されたルーチンをディスパッチする呼び出しを生成する\_ディスパッチします。

フィルターは、一時停止状態にグラフ遷移するときに、クロックを選択します。 たとえば、キャプチャ フィルターのプッシュ ソースには任意のフィルターには、クロック プロバイダーとして基本設定が与えられます。

 

 




