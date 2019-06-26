---
title: WIA\_IP\_ページ
description: WIA\_IP\_自動ドキュメント フィーダーから取得するページの現在の数がページのプロパティに含まれています。
ms.assetid: 638f816b-0efd-4885-b285-4fa6a42272bc
keywords:
- WIA_IPS_PAGES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d47cd0a6b495a0971f73117dfd6ac200736bc0b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385304"
---
# <a name="wiaipspages"></a>WIA\_IP\_ページ


WIA\_IP\_自動ドキュメント フィーダーから取得するページの現在の数がページのプロパティに含まれています。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲 (0 ~ ゼロ (0) に設定して、継続的にスキャン; スキャナーがスキャンできるページの最大数)

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションは、WIA を読み取ります\_IP\_ドキュメント フィーダー付きを確認するページのページの容量。 アプリケーションでは、このプロパティを WIA の現在のセッションでスキャンするページの最大数に設定します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表に、WIA で有効な定数\_IP\_ページ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ALL_PAGES</p></td>
<td><p>複数のドキュメントではありませんが、ADF に渡すまで継続的にスキャンします。 この値は、WIA_PROP_RANGE をゼロ (0) に設定すると同じです。</p></td>
</tr>
</tbody>
</table>

 

**注**  二重モードが有効になっている場合 (場合に、WIA\_IP\_ドキュメント\_処理\_フィーダーに設定されている選択 |双方向)、WIA\_IP\_ページは依然としてスキャンするページ数。
1 枚の用紙が自動的に入力 2 つのページ二重モードが有効になっている場合、ページの背面にある空白である場合でもです。

WIA を設定した場合\_IP\_を 1 に、スキャナーのページは、ページの側面の 1 つを処理します。 スキャナーは、二重モードでは、ページの一方だけをスキャンできない場合、WIA を変更する必要があります、ことをお勧めします\_IP\_ページ値、 **Inc**のメンバー、 [ **WIA。\_プロパティ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)構造体を 2 にします。 この値は、アプリケーションは 2 つの倍数単位のページを要求する必要があります。 値が 0 のことを意味*すべて*ドキュメント フィーダーに現在読み込まれているページがスキャンされるは。

 

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PAGES プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ**](wia-dps-pages.md)

[**WIA\_プロパティ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






