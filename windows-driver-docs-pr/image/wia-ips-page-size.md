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
ms.openlocfilehash: 95cf34fd77cf26fab0e9c56158b14ff36a1ab240
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330242"
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
<th>値</th>
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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PAGE_SIZE プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_IP\_向き**](wia-ips-orientation.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






