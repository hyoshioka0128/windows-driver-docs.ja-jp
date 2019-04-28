---
title: WIA\_IP\_DESKEW\_Y
description: WIA\_IP\_DESKEW\_Y プロパティを WIA と共に\_IP\_DESKEW\_プロパティ、X 傾斜したイメージの上の 2 つの角をについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 25aca00f-4048-4784-90a1-f1ad8c2de16a
keywords:
- WIA_IPS_DESKEW_Y イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_DESKEW_Y
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 927e4957661e93d3bdceb6227cd6a9498c2e39a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370606"
---
# <a name="wiaipsdeskewy"></a>WIA\_IP\_DESKEW\_Y


WIA\_IP\_DESKEW\_Y プロパティ、と共に、 [ **WIA\_IP\_DESKEW\_X** ](wia-ips-deskew-x.md)プロパティ傾斜したイメージの上の 2 つの角をについて説明します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_IP\_DESKEW\_X と WIA\_IP\_DESKEW\_Y プロパティは、傾斜したイメージの 2 つの上端は、外接する四角形内にある場所について説明する[**WIA\_IP\_XPOS**](wia-ips-xpos.md)、 [ **WIA\_IP\_YPOS**](wia-ips-ypos.md)、 [ **WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、および[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティを定義します。

WIA の有効な値\_IP\_DESKEW\_Y が 0 の間である必要があり、(WIA\_IP\_YEXTENT - 1)。 値の 0 の場合は deskew を実行しない必要があります。

WIA\_IP\_DESKEW\_Y には、WIA から y 方向のピクセルの数が含まれています。\_IP\_deskewed ありますする、イメージの一番左上隅の y 座標を YPOS します。

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


[**WIA\_IP\_DESKEW\_X**](wia-ips-deskew-x.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






