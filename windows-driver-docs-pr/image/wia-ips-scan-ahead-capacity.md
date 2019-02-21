---
title: WIA\_IP\_スキャン\_AHEAD\_容量
description: WIA\_IP\_スキャン\_AHEAD\_容量は、現在のスキャン ジョブ設定 (現在でスキャナーをスキャンして (したりする内部スキャナーのメモリ バッファーに格納) ページの最大数をについて説明しますドキュメント サイズ、解像度のスキャン、データ型、ファイル形式、圧縮、およびなど)。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 7A80964D-B0A4-4D6B-A320-4DE0A700E1A9
keywords:
- WIA_IPS_SCAN_AHEAD_CAPACITY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SCAN_AHEAD_CAPACITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b217831f3282502a17c0376a7ced3fa18f6e9ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531107"
---
# <a name="wiaipsscanaheadcapacity"></a>WIA\_IP\_スキャン\_AHEAD\_容量


**WIA\_IP\_スキャン\_AHEAD\_容量**スキャナーをスキャンして (したりする内部スキャナーのメモリ バッファーに格納) ページの最大数を現在のについて説明しますジョブの設定 (現在のドキュメント サイズ、スキャン解像度、データ型、ファイル形式、圧縮、およびなど) をスキャンします。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

ときに、 [ **WIA\_IP\_スキャン\_AHEAD** ](wia-ips-scan-ahead.md)プロパティがサポートされている、このプロパティは、フィーダー項目に対してのみ有効です (WIA\_カテゴリ\_フィーダー) では省略可能です。

値 0 は、「ページの未定義または不明な数です。」を意味します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





