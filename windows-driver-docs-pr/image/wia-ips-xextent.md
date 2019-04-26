---
title: WIA\_IP\_XEXTENT
description: WIA\_IP\_XEXTENT プロパティには、現在の幅 (ピクセル単位) を取得する、選択したイメージが含まれています。
ms.assetid: 00e8f705-5c2a-40ac-8635-b21a5d3315a3
keywords:
- WIA_IPS_XEXTENT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_XEXTENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c4ee7b524df501dcee8f7dc31fe04b6b14b190
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343864"
---
# <a name="wiaipsxextent"></a>WIA\_IP\_XEXTENT


WIA\_IP\_XEXTENT プロパティには、現在の幅 (ピクセル単位) を取得する、選択したイメージが含まれています。

## <span id="ddk_wia_ips_xextent_si"></span><span id="DDK_WIA_IPS_XEXTENT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_XEXTENT プロパティを取得する選択領域の左上隅 (つまり、幅) をマークします。 ミニドライバーは、作成し、このプロパティを保持します。

WIA\_IP\_XEXTENT 必須の取得を有効になっている項目とこれらの項目の子項目すべてのイメージではこのプロパティはストレージのアイテムまたはアイテムの保存されたイメージを使用できません。

ドライバーが、WIA を設定するのには、固定ページ サイズを設定すると、\_IP\_XEXTENT、 [ **WIA\_IP\_XPOS**](wia-ips-xpos.md)、 [ **WIA\_IP\_YEXTENT**](wia-ips-yextent.md)、および[ **WIA\_IP\_YPOS** ](wia-ips-ypos.md)ページ サイズに合わせてプロパティディメンションは、「0」の原点。 ドライバーがドキュメントの中央揃え、WIA を設定する\_IP\_に XPOS ((領域の幅のドキュメントの幅をスキャンする)/2)\*解決\[DPI\]) と WIA\_IP\_((YPOS領域の高さのドキュメントの高さをスキャン)/2)\*解決\[DPI\])。

ドライバーを更新するには、配信元または 1 つのエクステントが変更されたとき、 [ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)プロパティをカスタム\_サイズと、 [**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)と[ **WIA\_IP\_ページ\_高さ** ](wia-ips-page-height.md)にスキャンの領域のエクステントを対応するプロパティ。 印刷の向きと回転は、向きの変更 (回転変更ではありません)、配信元や、使用可能なドキュメントのスキャン領域外の 1 つのエクステントをレンダリングする場合を除き、これらのプロパティを影響する必要があります。

ドライバーは、更新、WIA もする必要があります\_IP\_XEXTENT、WIA\_IP\_XPOS、WIA\_IP\_YEXTENT、および WIA\_IP\_YPOS プロパティと[ **WIA\_IP\_XRES** ](wia-ips-xres.md)と[ **WIA\_IP\_YRES** ](wia-ips-yres.md)は変更されました。

**注**  ベッドと映画の子項目は、WIA のみをサポートする必要があります\_IP\_XEXTENT、WIA\_IP\_XPOS、WIA\_IP\_XRES、WIA\_IP\_YEXTENT、WIA\_IP\_YPOS、および WIA\_IP\_YRES プロパティ。 その他のプロパティ、必須またはオプション (基本ベッドまたはフィルムの項目)、その親のでは、これらの項目のオプションのみです。 唯一の例外は、WIA\_IPA\_項目\_*Xxx*プロパティで、すべての項目に必要な。

 

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


[**WIA\_IPA\_ピクセル\_1 秒あたり\_行**](wia-ipa-pixels-per-line.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_ページ\_幅**](wia-ips-page-width.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_XRES**](wia-ips-xres.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

[**WIA\_IP\_YRES**](wia-ips-yres.md)

 

 






