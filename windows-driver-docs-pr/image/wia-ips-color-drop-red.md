---
title: WIA\_IP\_色\_ドロップ\_赤
description: WIA\_IP\_色\_ドロップ\_赤いプロパティは、色の赤のカラー チャネル (R の RGB)、ドロップ アウトの量を構成する範囲は 0 (ドロップ アウト) ~ 100 (完全なチャネルのドロップ アウト) の割合として使用されます。
ms.assetid: B241154C-0F4F-4800-A8CD-30831F1AB25B
keywords:
- WIA_IPS_COLOR_DROP_RED イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_RED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4085ce5c989428efc2bba45728ef495e463b89c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325040"
---
# <a name="wiaipscolordropred"></a>WIA\_IP\_色\_ドロップ\_赤


**WIA\_IP\_色\_ドロップ\_RED**プロパティは、色の赤のカラー チャネル (R の RGB)、ドロップ アウトの量を構成する、0% (ドロップ アウト) の範囲内での割合として使用されます100% (フル チャネル ドロップ アウト)。 WIA ミニドライバーは、作成し、このプロパティを保持します。



プロパティの種類:VT\_I4 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

ときに、 [ **WIA\_IP\_色\_ドロップ**](wia-ips-color-drop.md)プロパティがサポートされている、このプロパティはベッド (WIA を含むすべてプログラミング可能なイメージのデータ ソース項目に対して無効です\_カテゴリ\_ベッド) とフィーダー (WIA\_カテゴリ\_フィーダー) 必要があります。 このプロパティの有効な値では、0 から 100 までの間です。

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

 

 





