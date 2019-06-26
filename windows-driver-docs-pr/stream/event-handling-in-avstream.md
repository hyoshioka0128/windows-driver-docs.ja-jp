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
ms.openlocfilehash: fbcaf79e53824e4300a852ecaf2b58789e291490
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384103"
---
# <a name="event-handling-in-avstream"></a>AVStream でのイベント処理





AVStream フィルターとピンは、プロパティ、イベント、および指定することによってサポートされる方法を説明します、 [ **KSAUTOMATION\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksautomation_table_)構造体、 **AutomationTable**のメンバーである、 [ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)構造または[ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 詳細については、次を参照してください。 [AVStream 記述子](avstream-descriptors.md)します。

配列を提供する、AVStream ミニドライバー イベントをサポートする[ **KSEVENT\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_set) automation テーブルの構造体。 各 KSEVENT\_セット構造体の配列を格納する[ **KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)構造体。 各 KSEVENT\_項目の構造は、ミニドライバーが特定のイベントをサポートする方法について説明します。

指定することによって、ミニドライバーがイベントの動作をカスタマイズできます[ *AVStrMiniAddEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksaddevent)と[ *AVStrMiniRemoveEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksremoveevent)ハンドラーで、KSEVENT\_項目の構造体。

イベントの有効化要求を受信すると、AVStream、KSEVENT が生成されます\_エントリの構造体。 ミニドライバーが指定されている場合、 *AVStrAddEvent*ハンドラー、AVStream にポインターを渡します、KSEVENT\_エントリの構造体への呼び出しで*AVStrAddEvent*します。

指定しない場合、 *AVStrAddEvent*ハンドラー、し、既定では AVStream イベントを追加、オブジェクトの一覧にします。 ミニドライバーは受信しません、 [ **KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)ポインター。 ミニドライバーは、呼び出すことによって、イベントをトリガーできる[ **KsFilterGenerateEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfiltergenerateevents)または[ **KsPinGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingenerateevents)します。

 

 




