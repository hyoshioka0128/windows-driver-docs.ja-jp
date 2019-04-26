---
title: WIA\_IP\_YSCALING
description: WIA\_IP\_YSCALING プロパティは、y 軸に沿ってスケーリングは、スキャンに適用するかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 4466697b-0d8e-477e-8dd0-2b277d4fd6b3
keywords:
- WIA_IPS_YSCALING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_YSCALING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f82dc8979ae3f6507f60ed346a570526a3534b54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357018"
---
# <a name="wiaipsyscaling"></a>WIA\_IP\_YSCALING


WIA\_IP\_YSCALING プロパティは、y 軸に沿ってスケーリングは、スキャンに適用するかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

有効な値、WIA\_IP\_YSCALING プロパティ 1 ~ 65535 の範囲。

WIA\_IP\_YSCALING は y 軸に沿ってスケーリングだけを示します。 画像を一様にスケールする場合は、WIA のような値を設定する必要があります\_IP\_YSCALING し、 [ **WIA\_IP\_XSCALING** ](wia-ips-xscaling.md)プロパティ。

次に例を示します。

-   100、スケーリングなし (100% x 1)。 イメージは変更されません。

-   050、1/2 の 50 %x (1/2) をスケールします。 イメージ サイズが 50% を y 軸に沿って減少 (1/2、元のサイズ)。

-   200、2 x (200%) をスケーリングします。 イメージのサイズは 200% (double)、y 軸に沿って拡大されます。

<a name="requirements"></a>必要条件
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


[**WIA\_IP\_XSCALING**](wia-ips-xscaling.md)

 

 






