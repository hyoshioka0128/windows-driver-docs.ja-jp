---
title: WIA\_DPS\_ページ\_幅
description: WIA\_DPS\_ページ\_WIDTH プロパティがインチの部分の 1/1000 で、現在選択されているページの幅が含まれています (. 001)。
ms.assetid: 02787660-3fb3-4e5d-ade8-b11ad29412c1
keywords:
- WIA_DPS_PAGE_WIDTH イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e447b1a5f4f0d0926f64250762629840f72be9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380948"
---
# <a name="wiadpspagewidth"></a>WIA\_DPS\_ページ\_幅


WIA\_DPS\_ページ\_WIDTH プロパティがインチの部分の 1/1000 で、現在選択されているページの幅が含まれています (. 001)。

## <span id="ddk_wia_dps_page_width_si"></span><span id="DDK_WIA_DPS_PAGE_WIDTH_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPS\_ページ\_WIDTH プロパティにスキャンされているページの物理的なサイズを決定します。 エクステント設定が既知のページ サイズと異なる場合、このプロパティは、ページの幅を報告が[ **WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)プロパティに設定WIA\_ページ\_カスタム。 WIA ミニドライバーを作成し、維持 WIA\_DPS\_ページ\_幅。

WIA\_DPS\_ページ\_幅の値に相当する測定値を提供する必要があります、 [ **WIA\_IP\_XEXTENT** ](wia-ips-xextent.md)プロパティ幅 (ピクセル単位) をスキャンするページのレポートします。

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
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降では、同じ WIA_IPS_PAGE_WIDTH プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ\_高さ**](wia-dps-page-height.md)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

 

 






