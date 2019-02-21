---
title: WIA\_IP\_YRES
description: WIA\_IP\_YRES プロパティには、デバイスの 1 インチあたりのピクセル単位で、現在の垂直方向の解像度設定が含まれています。
ms.assetid: 40a98cac-e5de-42db-b9df-1fba63925427
keywords:
- WIA_IPS_YRES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_YRES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964256c44e62ae2f4ee206c9f7323a76ab8ceb3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538484"
---
# <a name="wiaipsyres"></a>WIA\_IP\_YRES


WIA\_IP\_YRES プロパティには、デバイスの 1 インチあたりのピクセル単位で、現在の垂直方向の解像度設定が含まれています。

## <span id="ddk_wia_ips_yres_si"></span><span id="DDK_WIA_IPS_YRES_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_YRES プロパティ垂直方向の解像度を設定します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

デバイスは、値は 1 つだけに設定することができます、作成、WIA\_PROP\_リストの種類と、有効な値を配置します。 このような状況は、1 つの解像度の設定が別の解像度に依存する場合にも適用されます。 (たとえば、垂直方向の解像度に依存できます水平方向の解像度。)

WIA\_IP\_YRES はすべてのイメージの取得が有効な項目と項目の保存されたイメージに必要です。 ストレージ アイテムを使用できなくなります。

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


[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_XRES**](wia-ips-xres.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






