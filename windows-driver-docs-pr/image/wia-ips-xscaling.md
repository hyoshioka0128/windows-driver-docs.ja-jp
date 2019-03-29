---
title: WIA\_IP\_XSCALING
description: WIA\_IP\_XSCALING プロパティは、x 軸に沿ってスケーリングは、スキャンに適用するかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 608ac942-4a37-4490-8715-a1e2ebc4dc64
keywords:
- WIA_IPS_XSCALING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_XSCALING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eeb96b0fd3f4c9c429bcf216142db9da56d6cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569774"
---
# <a name="wiaipsxscaling"></a>WIA\_IP\_XSCALING


WIA\_IP\_XSCALING プロパティは、x 軸に沿ってスケーリングは、スキャンに適用するかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>コメント
-------

有効な値、WIA\_IP\_XSCALING プロパティ 1 ~ 65535 の範囲。

WIA\_IP\_XSCALING は x 軸に沿ってスケーリングだけを示します。 画像を一様にスケールする場合は、WIA のような値を設定する必要があります\_IP\_XSCALING し、 [ **WIA\_IP\_YSCALING** ](wia-ips-yscaling.md)プロパティ。

次に例を示します。

-   100、スケーリングなし (100% x 1)。 イメージは変更されません。

-   050、1/2 の 50 %x (1/2) をスケールします。 イメージ サイズが 50 %x 軸に沿った減少 (1/2、元のサイズ)。

-   200、2 x (200%) をスケーリングします。 イメージのサイズは 200% (double)、x 軸に沿って拡大されます。

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


[**WIA\_IP\_YSCALING**](wia-ips-yscaling.md)

 

 






