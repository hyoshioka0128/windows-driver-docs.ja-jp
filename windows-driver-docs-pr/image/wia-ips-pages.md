---
title: WIA\_IP\_ページ
description: WIA\_IP\_ページのプロパティには、自動ドキュメントフィーダーから取得する現在のページ数が含まれています。
ms.assetid: 638f816b-0efd-4885-b285-4fa6a42272bc
keywords:
- WIA_IPS_PAGES イメージングデバイス
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
ms.openlocfilehash: 72d237bb3fed1abcb74e01c97f0daf91fdd01c73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840684"
---
# <a name="wia_ips_pages"></a>WIA\_IP\_ページ


WIA\_IP\_ページのプロパティには、自動ドキュメントフィーダーから取得する現在のページ数が含まれています。

プロパティの型: VT\_I4

有効な値: WIA\_PROP\_RANGE (スキャナーがスキャンできる最大ページ数を0に設定します。連続スキャンするにはゼロ (0) に設定します。

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションでは、ドキュメントフィーダーのページ容量を決定するために、WIA\_IP\_ページを読み取ります。 アプリケーションは、このプロパティを、現在の WIA セッションでスキャンするページの最大数に設定します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。

次の表では、WIA\_IP\_ページで有効な定数について説明します。

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
<td><p>ADF にドキュメントが送られなくなるまで、継続的にスキャンします。 この値は、WIA_PROP_RANGE をゼロ (0) に設定した場合と同じです。</p></td>
</tr>
</tbody>
</table>

 

双方向モードが有効になっている場合 (つまり、WIA\_IP\_ドキュメント\_処理\_SELECT が [フィーダー] に設定されている場合は  ) に**注意**してください。両面)、WIA\_IP\_ページはスキャンするページ数と同じです。
両面が有効になっている場合、ページの裏面が空白の場合でも、1枚の用紙に自動的に2つのページが表示されます。

[WIA\_IP\_ページ] を1に設定すると、スキャナーはページのいずれかの辺を処理します。 スキャナーが両面モードでページの片面だけをスキャンできない場合は、wia [ **\_プロパティ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)構造体の**Inc**メンバーの [WIA\_ip\_ページ] の値を2に変更することをお勧めします。 この値を使用すると、アプリケーションは2つの倍数でページを要求する必要があります。 値が0の場合は、現在ドキュメントフィーダーに読み込まれている*すべて*のページがスキャンされます。

 

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
<td><p>Windows Vista 以降のオペレーティングシステムで使用できます。 Windows XP の場合は、代わりに WIA_DPS_PAGES プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ**](wia-dps-pages.md)

[**WIA\_プロパティ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






