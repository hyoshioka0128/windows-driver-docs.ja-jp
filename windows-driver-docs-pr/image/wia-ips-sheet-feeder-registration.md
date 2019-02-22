---
title: WIA\_IP\_シート\_フィーダー\_登録
description: WIA\_IP\_シート\_フィーダー\_REGISTRATION プロパティには、登録、または配置とエッジの検出、スキャナーのベッドに配置されているドキュメントが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: d97d5784-3360-48a3-a24e-97b4238c42f5
keywords:
- WIA_IPS_SHEET_FEEDER_REGISTRATION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SHEET_FEEDER_REGISTRATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc2516bbc397836a660921f9bc2689d224bf679d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551560"
---
# <a name="wiaipssheetfeederregistration"></a>WIA\_IP\_シート\_フィーダー\_登録


WIA\_IP\_シート\_フィーダー\_REGISTRATION プロパティには、登録、または配置とエッジの検出、スキャナーのベッドに配置されているドキュメントが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA\_IP\_シート\_フィーダー\_登録プロパティは、シート フィーダー型、またはハンドヘルド スキャナーのスキャニング ヘッドにドキュメントを水平方向に配置方法を示します。 WIA を使用する\_IP\_シート\_フィーダー\_スキャニング ヘッド間でドキュメントが配置されている予測に登録します。

次の表に、WIA で有効な定数\_IP\_シート\_フィーダー\_登録します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>定数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LEFT_JUSTIFIED</p></td>
<td><p>ドキュメントはスキャニング ヘッドに対して左に配置されます。</p></td>
</tr>
<tr class="even">
<td><p>中央揃え</p></td>
<td><p>ドキュメントは、スキャニング ヘッドの中央に配置します。</p></td>
</tr>
<tr class="odd">
<td><p>RIGHT_JUSTIFIED</p></td>
<td><p>ドキュメントはスキャニング ヘッドに対して右に配置されます。</p></td>
</tr>
</tbody>
</table>

 

1 つ以上をサポートするスキャナーをスキャン、WIA ヘッド\_IP\_シート\_フィーダー\_REGISTRATION プロパティは、最上位の基準としたスキャン head です。 このプロパティは、シートが取り込まれる、スクロールが取り込まれる、およびハンドヘルド スキャナーで必須です。

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_SHEET_FEEDER_REGISTRATION プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_シート\_フィーダー\_登録**](wia-dps-sheet-feeder-registration.md)

 

 






