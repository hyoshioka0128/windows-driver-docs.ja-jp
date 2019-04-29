---
title: WIA\_IP\_DESKEW\_X
description: WIA\_IP\_DESKEW\_プロパティと共に、WIA X\_IP\_DESKEW\_Y プロパティは、傾斜したイメージの上の 2 つの角をについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 0392d392-d814-4691-abb5-a8167bc101bb
keywords:
- WIA_IPS_DESKEW_X イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_DESKEW_X
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147d4e6ad75831fb3d3b3ffb42b6b357adcc20b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370701"
---
# <a name="wiaipsdeskewx"></a>WIA\_IP\_DESKEW\_X


WIA\_IP\_DESKEW\_と共に、プロパティの X、 [ **WIA\_IP\_DESKEW\_Y** ](wia-ips-deskew-y.md)プロパティ傾斜したイメージの上の 2 つの角をについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_IP\_DESKEW\_X と WIA\_IP\_DESKEW\_Y プロパティでは、傾斜したイメージの 2 つ上の角が外接する四角形内にあるかを記述しますその[。 **WIA\_IP\_XPOS**](wia-ips-xpos.md)、 [ **WIA\_IP\_YPOS**](wia-ips-ypos.md)、 [**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、および[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティを定義します。

WIA の有効な値\_IP\_DESKEW\_X が 0 の間である必要があり、(WIA\_IP\_XEXTENT - 1)。 値の 0 の場合は修正の傾斜を実行しない必要があります。

WIA\_IP\_DESKEW\_X には、WIA から x 方向のピクセルの数が含まれています。\_IP\_を修正する画像の上隅の x 座標を XPOS します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IP\_DESKEW\_Y**](wia-ips-deskew-y.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






