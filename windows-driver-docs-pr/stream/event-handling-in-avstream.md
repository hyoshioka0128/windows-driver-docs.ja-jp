---
title: AVStream でのイベント処理
description: AVStream でのイベント処理
ms.assetid: 7add2055-8d3f-432d-8aa1-44459ac197dd
keywords:
- WDK AVStream のイベント
- AVStream イベント WDK
- automation の WDK AVStream テーブルにします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28b24165e8b33c07030d7b4c97b11ff9f6d87a50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572687"
---
# <a name="event-handling-in-avstream"></a>AVStream でのイベント処理





AVStream フィルターとピンは、プロパティ、イベント、および指定することによってサポートされる方法を説明します、 [ **KSAUTOMATION\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff560990)構造体、 **AutomationTable**のメンバーである、 [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)構造または[ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 詳細については、次を参照してください。 [AVStream 記述子](avstream-descriptors.md)します。

配列を提供する、AVStream ミニドライバー イベントをサポートする[ **KSEVENT\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff561867) automation テーブルの構造体。 各 KSEVENT\_セット構造体の配列を格納する[ **KSEVENT\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff561862)構造体。 各 KSEVENT\_項目の構造は、ミニドライバーが特定のイベントをサポートする方法について説明します。

指定することによって、ミニドライバーがイベントの動作をカスタマイズできます[ *AVStrMiniAddEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff554260)と[ *AVStrMiniRemoveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff556361)ハンドラーで、KSEVENT\_項目の構造体。

イベントの有効化要求を受信すると、AVStream、KSEVENT が生成されます\_エントリの構造体。 ミニドライバーが指定されている場合、 *AVStrAddEvent*ハンドラー、AVStream にポインターを渡します、KSEVENT\_エントリの構造体への呼び出しで*AVStrAddEvent*します。

指定しない場合、 *AVStrAddEvent*ハンドラー、し、既定では AVStream イベントを追加、オブジェクトの一覧にします。 ミニドライバーは受信しません、 [ **KSEVENT\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff561853)ポインター。 ミニドライバーは、呼び出すことによって、イベントをトリガーできる[ **KsFilterGenerateEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff562541)または[ **KsPinGenerateEvents**](https://msdn.microsoft.com/library/windows/hardware/ff563500)します。

 

 




