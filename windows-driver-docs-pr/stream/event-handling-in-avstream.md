---
title: AVStream でのイベント処理
description: AVStream でのイベント処理
ms.assetid: 7add2055-8d3f-432d-8aa1-44459ac197dd
keywords:
- イベント WDK AVStream
- AVStream イベント WDK
- automation テーブル WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ea9dd5581d657bd38a0b274c51c01296d2f1bfc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826210"
---
# <a name="event-handling-in-avstream"></a>AVStream でのイベント処理





AVStream のフィルターとピンは、 [**Ksautomation\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)構造を指定してサポートするプロパティ、イベント、およびメソッドについて説明**します。これは、** [**ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体また[**はKSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体です。 詳細については、「 [Avstream 記述子](avstream-descriptors.md)」を参照してください。

イベントをサポートするために、AVStream ミニドライバーは、オートメーションテーブルに[**KSEVENT\_セット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_set)構造の配列を提供します。 各 KSEVENT\_SET 構造体には、 [**KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)構造体の配列が含まれています。 各 KSEVENT\_項目構造では、ミニドライバーが特定のイベントをサポートする方法について説明します。

ミニドライバーを使用すると、 [*Avstrminiaddevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksaddevent)と[*AVSTRMINIKSEVENT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksremoveevent)を\_ITEM 構造体に渡すことで、イベントの動作をカスタマイズできます。

AVStream は、イベント有効化要求を受け取ると、KSEVENT\_エントリ構造を生成します。 ミニドライバーに*avstraddevent*ハンドラーが指定されている場合、Avstream は*avstraddevent*への呼び出しで KSEVENT\_ENTRY 構造体へのポインターを渡します。

*Avstraddevent*ハンドラーが指定されていない場合は、既定で avstream によってイベントがオブジェクトリストに追加されます。 ミニドライバーは、 [**KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)ポインターを受け取りません。 ミニドライバーは、 [**Ksfiltergenerateevents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltergenerateevents)または[**KsPinGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingenerateevents)を呼び出すことによってイベントをトリガーできます。

 

 




