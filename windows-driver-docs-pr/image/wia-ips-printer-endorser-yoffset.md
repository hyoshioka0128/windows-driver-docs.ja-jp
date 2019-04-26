---
title: WIA\_IP\_プリンター\_裏書き\_Y オフセット
description: WIA\_IP\_プリンター\_裏書き\_y オフセット プロパティがインチの後続の垂直方向の座標を構成に使用されます (0.001 \ 0034;)、imprinting/動作保証済み領域の左上隅のスキャンする物理的なドキュメントの左上隅にあると彫り動作保証済み。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: C04A4EAC-237A-44D6-AB05-CD561DA72CE8
keywords:
- WIA_IPS_PRINTER_ENDORSER_YOFFSET イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_YOFFSET
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e873d5c7b8dedb085479e9a3ae7ac5b6f3542e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353320"
---
# <a name="wiaipsprinterendorseryoffset"></a>WIA\_IP\_プリンター\_裏書き\_Y オフセット


**WIA\_IP\_プリンター\_裏書き\_y オフセット**の左上隅の 1/10、1/100、1/1000 インチ (0.001 インチ) 単位で垂直方向の座標を構成するプロパティを使用しますimprinting/動作保証済み領域、スキャンする物理的なドキュメントと彫り動作保証済みの左上隅に対して相対的です。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

WIA ミニドライバーを更新できます有効な値と現在の値の範囲 (範囲外となる) 場合に最も近い利用可能な位置と、 [ **WIA\_IP\_プリンター\_裏書き** ](wia-ips-printer-endorser.md) (つまり、フィーダーにベッド) から新しい特定の入力ソースにプロパティが変更されます。

このプロパティは・ インプリント ・/裏書きデータ ソース アイテムをすべて省略可能です。

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

 

 





