---
title: ワイルドカード
description: ワイルドカード
ms.assetid: fc42fb2d-8df9-47d6-9034-c0588ee81c95
keywords:
- 交差部分のデータ ハンドラーの WDK オーディオ、ワイルド カード
- ワイルドカードの WDK オーディオ
- データの範囲は WDK オーディオ、ワイルド カード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0634f49d3f60dec7ff690f6dd72cf29d149dfe73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552737"
---
# <a name="wild-cards"></a>ワイルドカード


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


Ks.h ヘッダー ファイルの次のワイルドカード パラメーターを定義する[ **KS データ範囲**](https://msdn.microsoft.com/library/windows/hardware/ff561658):

-   KSDATAFORMAT\_型\_ワイルドカード

-   KSDATAFORMAT\_サブタイプ\_ワイルドカード

-   KSDATAFORMAT\_指定子\_ワイルドカード

**MajorFormat**、**サブフォーマット**、および**指定子**のメンバー、 **DataRange**のメンバー、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)構造体は、これらの値に設定することができます。 ワイルド カードでは、先が比較される、将来的に定義することがすべてのデータ形式を含む任意の対応する値と一致します。 データ形式を理解することがなくデータを移動するシステムのフィルターとは、ワイルドカードのプライマリ ユーザーです。 アダプターのドライバーのフィルター pin のデータ範囲のワイルドカードを指定することを避ける必要がありますが、ピンがクライアントのフィルターのデータの範囲でワイルドカードを受け入れるように、準備する必要があります。

 

 




