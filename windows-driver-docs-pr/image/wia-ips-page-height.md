---
title: WIA\_IP\_ページ\_高さ
description: WIA\_IP\_ページ\_1/1000 インチの高さが高さのプロパティに含まれています (. 001)、現在選択されているページの。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: f8721f87-641c-4da8-ad3a-a38bf18d3111
keywords:
- WIA_IPS_PAGE_HEIGHT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 572747fc78b38c0af4ea6c04d4166b0c3430eba1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574278"
---
# <a name="wiaipspageheight"></a>WIA\_IP\_ページ\_高さ


WIA\_IP\_ページ\_1/1000 インチの高さが高さのプロパティに含まれています (. 001)、現在選択されているページの。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

アプリケーションは、WIA を読み取ります\_IP\_ページ\_スキャンされているページの物理的なサイズを決定する高さ。 エクステント設定が既知のページ サイズと異なる場合、このプロパティは、ページの高さを報告が[ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)プロパティは、WIA を設定\_ページ\_カスタム。

WIA\_IP\_ページ\_高さによって報告されるピクセル値と等価のインチの 1/10、1/100、1/1000 での測定値を指定する必要があります[ **WIA\_IP\_YEXTENT**](wia-ips-yextent.md)高さ、ピクセル単位で、スキャンするページのレポートします。

**注**  WIA サービス内で互換レイヤーは、WIA のサポートを追加していない\_IP\_ページ\_高さプロパティの場合は、Windows XP WIA デバイスから変換されたです、ADF 項目をプロパティデバイスの子項目ではサポートされません。 アプリケーションは、ADF の項目が常に WIA をサポートを期待できません\_IP\_ページ\_高さかどうかは、実行時にサポートを常に確認する必要があります。 (アプリケーション通常を確認するこのネゴシエートされる任意のプロパティのサポート。)

 

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PAGE_HEIGHT プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ\_高さ**](wia-dps-page-height.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

 

 






