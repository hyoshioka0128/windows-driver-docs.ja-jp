---
title: WIA\_IP\_YPOS
description: WIA\_IP\_YPOS プロパティには、現在座標 y 座標、選択したイメージの左上隅の (ピクセル単位) にはが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: e6592d54-d1b6-4ee7-8678-903d575d52a3
keywords:
- WIA_IPS_YPOS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_YPOS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d6867205c28896c78285a7d9eccf727dafd858
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551000"
---
# <a name="wiaipsypos"></a>WIA\_IP\_YPOS


WIA\_IP\_YPOS プロパティには、現在座標 y 座標、選択したイメージの左上隅の (ピクセル単位) にはが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_ypos_si"></span><span id="DDK_WIA_IPS_YPOS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_YPOS プロパティ選択領域の左上隅をマークします。

WIA\_IP\_YPOS 必須のすべてのイメージの取得が有効な項目とこれらの項目の子項目ではこのプロパティはストレージのアイテムまたはアイテムの保存されたイメージを使用できません。

ドライバーを設定するのには固定ページ サイズが設定されている場合、 [ **WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、 [ **WIA\_IP\_XPOS** ](wia-ips-xpos.md)、 [ **WIA\_IP\_YEXTENT**](wia-ips-yextent.md)、および**WIA\_IP\_YPOS**ディメンションと原点を「0」、ページと一致するプロパティのサイズします。 ドライバーがドキュメントの中央揃え、WIA を設定する\_IP\_に XPOS ((領域の幅のドキュメントの幅をスキャンする)/2)\*解決\[DPI\]) と WIA\_IP\_((YPOS領域の高さのドキュメントの高さをスキャン)/2)\*解決\[DPI\])。

ドライバーを更新するには、配信元または 1 つのエクステントが変更されたとき、 [ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)プロパティをカスタム\_サイズと、 [**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)と[ **WIA\_IP\_ページ\_高さ** ](wia-ips-page-height.md)にスキャンの領域のエクステントを対応するプロパティ。 印刷の向きと回転は、向きの変更 (回転変更ではありません)、配信元や、使用可能なドキュメントのスキャン領域外の 1 つのエクステントをレンダリングする場合を除き、これらのプロパティを影響する必要があります。

ドライバーは、WIA も更新する必要があります\_IP\_XEXTENT、WIA\_IP\_XPOS、WIA\_IP\_YEXTENT、および WIA\_IP\_YPOS プロパティと、 [ **WIA\_IP\_XRES** ](wia-ips-xres.md)と[ **WIA\_IP\_YRES** ](wia-ips-yres.md)プロパティが変更されます。

**注**   WIA のみをサポートするために必要な子項目のフラット ベッドと映画\_IP\_XEXTENT、WIA\_IP\_XPOS、WIA\_IP\_XRES、WIA\_IP\_YEXTENT、WIA\_IP\_YPOS、および WIA\_IP\_YRES プロパティ。 その他のプロパティ、必須またはオプション (基本ベッドまたはフィルムの項目)、その親のでは、これらの項目のオプションのみです。 唯一の例外は、WIA\_IPA\_項目\_*Xxx*プロパティで、すべての項目に必要な。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_XRES**](wia-ips-xres.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YRES**](wia-ips-yres.md)

 

 






