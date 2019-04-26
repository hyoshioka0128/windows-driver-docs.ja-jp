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
ms.openlocfilehash: 344d17361e2285904d85335e53d89f9622b9b98a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352700"
---
# <a name="avstream-clocks"></a>AVStream のクロック





AVStream のフィルターでは、pin でのクロックがサポートされます。

で、AVStream 暗証番号 (pin) が時計を公開していることを示す設定 KSPIN\_フラグ\_実装\_出勤、**フラグ**最初のメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)で、 **PinDescriptors**のメンバー [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553).

ポインターを提供する[ **KSCLOCK\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff561017)構造体[ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)します。

クロックの要求で定義されたメソッドを使用して、 [IKsReferenceClock](https://msdn.microsoft.com/library/windows/hardware/ff560725)インターフェイス。 取得することができます、 *IKsReferenceClock*呼び出してインターフェイス[ **KsPinGetReferenceClockInterface**](https://msdn.microsoft.com/library/windows/hardware/ff563517)します。 AVStream ミニドライバーが完了すると、インターフェイスを解放します。

配置するタイマー値を取得する、 **PresentationTime**フィールド[ **KSSTREAM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff567138)、呼び出す[ **IKsReferenceClock::GetCorrelatedTime**](https://msdn.microsoft.com/library/windows/hardware/ff560728)します。

クロックが選択されている場合でも、クロックが決して GraphEdit に表示されることに注意してください。

クロックが選択されていることを確認するへの呼び出しを確認します。 [IKsReferenceClock](https://msdn.microsoft.com/library/windows/hardware/ff560725)メソッド KSCLOCK で指定されたルーチンをディスパッチする呼び出しを生成する\_ディスパッチします。

フィルターは、一時停止状態にグラフ遷移するときに、クロックを選択します。 たとえば、キャプチャ フィルターのプッシュ ソースには任意のフィルターには、クロック プロバイダーとして基本設定が与えられます。

 

 




