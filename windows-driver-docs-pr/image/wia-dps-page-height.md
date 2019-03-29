---
title: WIA\_DPS\_ページ\_高さ
description: WIA\_DPS\_ページ\_1/1000 インチの高さが高さのプロパティに含まれています (. 001)、現在選択されているページの。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 93970d9a-96fe-4cf9-98c6-4ddcfd425214
keywords:
- WIA_DPS_PAGE_HEIGHT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a589ca1199be8449996903ab155a35f5f771cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570665"
---
# <a name="wiadpspageheight"></a>WIA\_DPS\_ページ\_高さ


WIA\_DPS\_ページ\_1/1000 インチの高さが高さのプロパティに含まれています (. 001)、現在選択されているページの。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dps_page_height_si"></span><span id="DDK_WIA_DPS_PAGE_HEIGHT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

アプリケーションの読み取り WIA\_DPS\_ページ\_スキャンされているページの物理的なサイズを決定する高さ。 エクステント設定が既知のページ サイズと異なる場合、このプロパティは、ページの高さを報告が[ **WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)プロパティは、WIA に設定\_ページ\_カスタム (これは、値、WIA の\_DPS\_ページ\_SIZE プロパティ)。

WIA\_DPS\_ページ\_高さによって報告されたピクセル値と等価のインチの 1/10、1/100、1/1000 での測定値を指定する必要があります、 [ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティで、スキャンするページのピクセルの高さを報告します。

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
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降では、同じ WIA_IPS_PAGE_HEIGHT プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

 

 






