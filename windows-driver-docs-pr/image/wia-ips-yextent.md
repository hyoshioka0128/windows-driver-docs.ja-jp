---
title: WIA\_IP\_YEXTENT
description: WIA\_IP\_YEXTENT プロパティには、現在の高さ (ピクセル単位) を取得する、選択したイメージが含まれています。
ms.assetid: 3d07d7d0-a590-49ed-a3d4-c873997b9c27
keywords:
- WIA_IPS_YEXTENT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_YEXTENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d99b092aa5168cf3182c02bcd03dd112355a2ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325039"
---
# <a name="wiaipsyextent"></a>WIA\_IP\_YEXTENT


WIA\_IP\_YEXTENT プロパティには、現在の高さ (ピクセル単位) を取得する、選択したイメージが含まれています。

## <span id="ddk_wia_ips_yextent_si"></span><span id="DDK_WIA_IPS_YEXTENT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_YEXTENT プロパティを取得する選択領域の左上隅 (つまり、高さ) をマークします。 WIA ミニドライバーは、作成し、このプロパティを保持します。

WIA\_IP\_YEXTENT 必須の取得を有効になっている項目とこれらの項目の子項目すべてのイメージではこのプロパティはストレージのアイテムまたはアイテムの保存されたイメージを使用できません。

ドライバーを設定するのには固定ページ サイズが設定されている場合、 [ **WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、 [ **WIA\_IP\_XPOS** ](wia-ips-xpos.md)、WIA\_IP\_YEXTENT、および[ **WIA\_IP\_YPOS** ](wia-ips-ypos.md)ページと一致するプロパティサイズの寸法と「0」の原点。 ドライバーがドキュメントの中央揃え、WIA を設定する\_IP\_に XPOS ((領域の幅のドキュメントの幅をスキャンする)/2)\*解決\[DPI\]) と WIA\_IP\_((YPOS領域の高さのドキュメントの高さをスキャン)/2)\*解決\[DPI\])。

ドライバーを更新するには、配信元または 1 つのエクステントが変更されたとき、 [ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)カスタム\_サイズと、 [ **WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)と[ **WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)にスキャンの領域のエクステントを対応するプロパティ。 印刷の向きと回転は、向きの変更 (回転変更ではありません)、配信元や、使用可能なドキュメントのスキャン領域外の 1 つのエクステントをレンダリングする場合を除き、これらのプロパティを影響する必要があります。

ドライバーを更新する必要がありますも、 [ **WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、WIA\_IP\_XPOS、WIA\_IP\_YEXTENT、および WIA\_IP\_YPOS プロパティと、 [ **WIA\_IP\_XRES** ](wia-ips-xres.md)と[ **WIA\_IP\_YRES** ](wia-ips-yres.md)プロパティが変更されます。

**注**   WIA のみをサポートするために必要な子項目のフラット ベッドと映画\_IP\_XEXTENT、WIA\_IP\_XPOS、WIA\_IP\_XRES、WIA\_IP\_YEXTENT、WIA\_IP\_YPOS、および WIA\_IP\_YRES プロパティ。 その他のプロパティ、必須またはオプション (基本ベッドまたはフィルムの項目)、その親のでは、これらの項目のオプションのみです。 唯一の例外は、WIA\_IPA\_項目\_*Xxx*プロパティで、すべての項目に必要な。

 

<a name="requirements"></a>必要条件
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


[**WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_XRES**](wia-ips-xres.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

[**WIA\_IP\_YRES**](wia-ips-yres.md)

 

 






