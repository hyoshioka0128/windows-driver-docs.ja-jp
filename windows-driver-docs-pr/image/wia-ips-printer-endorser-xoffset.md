---
title: WIA\_IP\_プリンター\_裏書き\_X オフセット
description: WIA\_IP\_プリンター\_裏書き\_1/10、1/100、1/1000 インチで水平方向の座標を構成する x オフセット プロパティが使用される (0.001 \ 0034;)、imprinting/動作保証済み領域の左上隅のスキャンする物理的なドキュメントの左上隅にあると彫り動作保証済み。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 3B3E1A02-0401-455C-B341-37FBEB108E4F
keywords:
- WIA_IPS_PRINTER_ENDORSER_XOFFSET イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_XOFFSET
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 969c7ecbf3b3aa50f5102ec371a4054cdf0ef728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391106"
---
# <a name="wiaipsprinterendorserxoffset"></a>WIA\_IP\_プリンター\_裏書き\_X オフセット


**WIA\_IP\_プリンター\_裏書き\_x オフセット**の左上隅の 1/10、1/100、1/1000 インチ (0.001 インチ) 単位で水平方向の座標を構成するプロパティを使用しますimprinting/動作保証済み領域、スキャンする物理的なドキュメントと彫り動作保証済みの左上隅に対して相対的です。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

WIA ミニドライバーを更新できます有効な値と現在の値の範囲 (範囲外となる) 場合に最も近い利用可能な位置と、 [ **WIA\_IP\_プリンター\_裏書き** ](wia-ips-printer-endorser.md) (つまり、フィーダーにベッド) から新しい特定の入力ソースにプロパティが変更されます。

このプロパティは・ インプリント ・/裏書きデータ ソース アイテムをすべて省略可能です。

<a name="requirements"></a>必要条件
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

 

 





