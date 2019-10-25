---
title: WIA\_IP\_ページ\_サイズ
description: '[WIA\_IP\_ページ\_サイズ] プロパティには、スキャン対象として現在選択されているページのサイズが表示されます。'
ms.assetid: dcfad67e-31d5-41b8-b471-532626f571af
keywords:
- WIA_IPS_PAGE_SIZE イメージングデバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0fc873135dcd03e0e9e83d299cdfe7301720e17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840682"
---
# <a name="wia_ips_page_size"></a>WIA\_IP\_ページ\_サイズ


[WIA\_IP\_ページ\_サイズ] プロパティには、スキャン対象として現在選択されているページのサイズが表示されます。

プロパティの型: VT\_I4

有効な値: WIA\_PROP\_LIST

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

スキャンするページのサイズを選択するために、アプリケーションは\_SIZE プロパティ\_[WIA\_IP] を設定します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。

次の表では、WIA\_IP\_ページ\_サイズで有効な定数について説明します。

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
<td><p>WIA_PAGE_A4</p></td>
<td><p>8267× 11692 (縦向き)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_AUTO</p></td>
<td><p>ページサイズの自動検出を構成するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p><a href="wia-ips-page-height.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_HEIGHT&lt;/strong&gt;](wia-ips-page-height.md)"><strong>WIA_IPS_PAGE_HEIGHT</strong></a>プロパティと<a href="wia-ips-page-width.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_WIDTH&lt;/strong&gt;](wia-ips-page-width.md)"><strong>WIA_IPS_PAGE_WIDTH</strong></a>プロパティの値によって定義されます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM_BASE</p></td>
<td><p>WIA_IPS_PAGE_HEIGHT プロパティと WIA_IPS_PAGE_WIDTH プロパティの値によって定義されます。 この値は、WIA_PAGE_CUSTOM 値によって有効になる単一ページではなく、カスタムページサイズを定義するために使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>8500× 11000 (縦向き)。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>Windows Vista 以降のオペレーティングシステムで使用できます。 Windows XP の場合は、代わりに WIA_DPS_PAGE_SIZE プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrv::d rvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IP\_ページ\_の高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






