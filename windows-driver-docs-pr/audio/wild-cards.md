---
title: ワイルド カード
description: ワイルド カード
ms.assetid: fc42fb2d-8df9-47d6-9034-c0588ee81c95
keywords:
- データの交差ハンドラー WDK オーディオ、ワイルドカード
- ワイルドカード WDK オーディオ
- データ範囲 WDK オーディオ、ワイルドカード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb498da0e0a00515aacab32141829e5a333209cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832231"
---
# <a name="wild-cards"></a>ワイルド カード


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


ヘッダーファイル Ks は、 [**ks データ範囲**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の次のワイルドカードパラメーターを定義します。

-   KSDATAFORMAT\_TYPE\_ワイルドカード

-   KSDATAFORMAT\_サブタイプ\_ワイルドカード

-   KSDATAFORMAT\_指定子\_ワイルドカード

[**Ksk Datarange の\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体の**datarange**メンバーの、、 **subformat**、および**指定子**のメンバーは、これらの値に設定できます。 ワイルドカードは、将来定義される可能性のあるデータ形式を含め、比較対象の対応する値と一致します。 データ形式を理解せずにデータを移動できるシステムフィルターは、ワイルドカードのプライマリユーザーです。 アダプタードライバーでは、フィルターの pin のデータ範囲にワイルドカードを指定する必要はありませんが、クライアントフィルターの pin のデータ範囲では、ワイルドカードを受け入れるように準備する必要があります。

 

 




