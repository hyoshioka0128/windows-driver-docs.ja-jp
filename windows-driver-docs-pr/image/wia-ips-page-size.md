---
title: WIA\_IP\_ページ\_サイズ
description: WIA\_IP\_ページ\_サイズ プロパティには、スキャンする現在選択されているページのサイズが含まれています。
ms.assetid: dcfad67e-31d5-41b8-b471-532626f571af
keywords:
- WIA_IPS_PAGE_SIZE イメージング デバイス
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
ms.openlocfilehash: 9fd171f04e8ea595886236fd3aad2709d64763f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385305"
---
# <a name="wiaipspagesize"></a>WIA\_IP\_ページ\_サイズ


WIA\_IP\_ページ\_サイズ プロパティには、スキャンする現在選択されているページのサイズが含まれています。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA をスキャンするページの寸法を選択する\_IP\_ページ\_SIZE プロパティ。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表に、WIA で有効な定数\_IP\_ページ\_サイズ。

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
<td><p>8267 × 11692 (縦向き)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_AUTO</p></td>
<td><p>ページの自動サイズの検出を構成するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>値によって定義された、 <a href="wia-ips-page-height.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_HEIGHT&lt;/strong&gt;](wia-ips-page-height.md)"> <strong>WIA_IPS_PAGE_HEIGHT</strong> </a>と<a href="wia-ips-page-width.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_WIDTH&lt;/strong&gt;](wia-ips-page-width.md)"> <strong>WIA_IPS_PAGE_WIDTH</strong> </a>プロパティ。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM_BASE</p></td>
<td><p>WIA_IPS_PAGE_HEIGHT および WIA_IPS_PAGE_WIDTH プロパティの値によって定義されます。 この値は、WIA_PAGE_CUSTOM 値を有効にする 1 つのページではなく、カスタム ページのサイズを定義に使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>8500 × 11000 (縦向き)。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PAGE_SIZE プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrv::drvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_IP\_向き**](wia-ips-orientation.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






