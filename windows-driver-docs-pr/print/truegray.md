---
title: TrueGray
description: TrueGray
ms.assetid: d6fef790-79d9-4ea7-8e1d-bca8837108de
keywords:
- ミニドライバー WDK Pscript、TrueGray 機能
- TrueGray 機能
- RGB 色の WDK プリンター
- 色の灰色の領域 WDK Pscript
- ADTrueGray
- 色の WDK Pscript のチェック
- RGB 色をチェック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb50f3a47009a33b06cfb6388926557d8154ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384952"
---
# <a name="truegray"></a>TrueGray





TrueGray 機能は、テキストとベクター グラフィックスがビットマップには、RGB 色を確認します。 色の灰色 (赤、緑、および青の値を持つが等しい色) である場合は、TrueGray 機能は、印刷する前に、RGB 色空間から、カラー プリンターの色の灰色の領域の色を変換します。 この機能は、モノクロ プリンターをご利用いただけません。

TrueGray 機能はプライベート*PPD*キーワード、 \* **ADTrueGray**PScript ミニドライバーのライターを有効またはこの機能を無効にすることを許可する。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>キーワードと値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>ADTrueGray</strong>:True</p></td>
<td><p>TrueGray 機能は、このプリンターの既定で有効です。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADTrueGray</strong>:False</p></td>
<td><p>既定ではこのプリンタの TrueGray 機能は無効です。</p></td>
</tr>
</tbody>
</table>

 

ドライバーがどの R の RGB 色を検出するときに、ユーザー インターフェイスでは、TrueGray 機能が有効になっていることを示します、G = = B と同じ場合、次の条件のいずれかです。

-   ICM の処理がオフの場合

-   場合 ICM 処理が、ホストで実行および変換先のカラー プロファイルは RGB データと変換後の色は、R' G =' B' を = (つまり、元の色から別)

-   ときに ICM 処理は通常どおり行われます CIE に基づく色空間と元の色を使用して R は、G = = B

CMYK カラーで灰色の検出は行われません。 これは、通常 ICM 色の処理が、ホストで実行するときに使用する色空間です。

 

 




