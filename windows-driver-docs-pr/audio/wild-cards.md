---
title: ワイルド カード
description: ワイルド カード
ms.assetid: fc42fb2d-8df9-47d6-9034-c0588ee81c95
keywords:
- 交差部分のデータ ハンドラーの WDK オーディオ、ワイルド カード
- ワイルドカードの WDK オーディオ
- データの範囲は WDK オーディオ、ワイルド カード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a31972735db8493c7d3769daae721f9a702951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364784"
---
# <a name="wild-cards"></a>ワイルド カード


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


Ks.h ヘッダー ファイルの次のワイルドカード パラメーターを定義する[ **KS データ範囲**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)):

-   KSDATAFORMAT\_型\_ワイルドカード

-   KSDATAFORMAT\_サブタイプ\_ワイルドカード

-   KSDATAFORMAT\_指定子\_ワイルドカード

**MajorFormat**、**サブフォーマット**、および**指定子**のメンバー、 **DataRange**のメンバー、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体は、これらの値に設定することができます。 ワイルド カードでは、先が比較される、将来的に定義することがすべてのデータ形式を含む任意の対応する値と一致します。 データ形式を理解することがなくデータを移動するシステムのフィルターとは、ワイルドカードのプライマリ ユーザーです。 アダプターのドライバーのフィルター pin のデータ範囲のワイルドカードを指定することを避ける必要がありますが、ピンがクライアントのフィルターのデータの範囲でワイルドカードを受け入れるように、準備する必要があります。

 

 




