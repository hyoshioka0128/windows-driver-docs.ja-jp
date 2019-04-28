---
title: ヘッダーとデータを分割する場所
description: ヘッダーとデータを分割する場所
ms.assetid: e302fcc1-5088-4f64-b454-5f20c69c0626
keywords:
- ヘッダー データの分割、WDK を分割する位置
- ネットワークを分割する位置を WDK を分割するイーサネット フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7288e9b056e0e569fb4980b877965cef30e8987d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365724"
---
# <a name="where-to-split-header-and-data"></a>ヘッダーとデータを分割する場所





次に、唯一の有効な場所ヘッダー データの分割プロバイダーが、イーサネット フレームを分割できます。

-   [上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。

-   [UDP ペイロードの先頭](splitting-frames-at-the-udp-payload.md)します。

-   [TCP ペイロードの先頭](splitting-frames-at-the-tcp-payload.md)します。

**注**  ヘッダー データの分割のプロバイダーにのみ、これらの要件が適用されます。 ヘッダー データの分割が使用されていない場合にフレームを分割の詳細については、次を参照してください。[の場合、ヘッダー データ分割が使用されていない](cases-where-header-data-split-is-not-used.md)します。

 

次の図は、イーサネット フレームと有効な分割の場所の主要な部分を示しています。

![wep アルゴリズムを使用して暗号化 mpdu 802.11 フレームの形式を示す図](images/hdsplitframe.png)

 

 





