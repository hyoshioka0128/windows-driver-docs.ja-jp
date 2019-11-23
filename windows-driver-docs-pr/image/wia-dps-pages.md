---
title: WIA\_DPS\_ページ
description: WIA の\_DPS\_ページのプロパティには、自動ドキュメントフィーダーから取得する現在のページ数が含まれます。
ms.assetid: 51ab2eab-c7b4-4d54-bfc7-d53a8f66c7a9
keywords:
- WIA_DPS_PAGES イメージングデバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c456ebb34f89c3f12f4dd4a981e6ebfda733a4f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840714"
---
# <a name="wia_dps_pages"></a>WIA\_DPS\_ページ


WIA の\_DPS\_ページのプロパティには、自動ドキュメントフィーダーから取得する現在のページ数が含まれます。

## <span id="ddk_wia_dps_pages_si"></span><span id="DDK_WIA_DPS_PAGES_SI"></span>


プロパティの型: VT\_I4

有効な値: WIA\_PROP\_範囲 (0 から、スキャナーがスキャンできる最大ページ数まで)。連続してスキャンする場合は 0 \[\] 0 に設定します。

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションは、WIA\_DPS\_PAGES プロパティを読み取って、ドキュメントフィーダーのページ容量を決定します。 また、アプリケーションは、スキャンするページ数にこのプロパティを設定します。 WIA ミニドライバーは、WIA\_DPS\_ページを作成し、管理します。

次の表では、WIA\_DPS\_PAGES プロパティで有効な定数について説明します。

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
<td><p>設定と同様に、をゼロ (0) に WIA_PROP_RANGE ます。 すべてのページ。 ADF にドキュメントが送られなくなるまで、継続的にスキャンします。</p></td>
</tr>
</tbody>
</table>

 

双方向モードが有効になっている場合 (つまり、 [**WIA\_DPS\_ドキュメント\_処理\_SELECT**](wia-dps-document-handling-select.md)プロパティが [フィーダー] に設定されている**場合  ** 両面)、WIA\_DPS\_ページは、スキャンするページ数と同じです。
両面が有効になっている場合、ページの裏面が空白の場合でも、1枚の用紙に自動的に2つのページが表示されます。

WIA\_DPS\_ページを1に設定すると、スキャナーはページのいずれかの辺を処理します。 スキャナーが両面モードで1つのページのみをスキャンできない場合は、wia [ **\_プロパティ\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)構造体の**Inc**メンバーの [WIA\_DPS\_PAGES] の値を2に変更する必要があります。 この値は、2の倍数でページを要求する必要があることをアプリケーションに通知します。 WIA\_DPS\_ページがゼロの場合、スキャナーは現在ドキュメントフィーダーに読み込まれている*すべて*のページをスキャンします。

 

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
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降の場合は、同一の WIA_IPS_PAGES プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ドキュメント\_処理\_選択**](wia-dps-document-handling-select.md)

[**WIA\_IP\_ページ**](wia-ips-pages.md)

[**WIA\_プロパティ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






