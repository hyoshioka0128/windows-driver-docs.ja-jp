---
title: WIA\_IP\_XRES
description: WIA\_IP\_XRES プロパティには、水平方向のデバイスの 1 インチあたりのピクセル単位で現在の解像度が含まれています。
ms.assetid: cde64e80-b4b0-4360-a14e-b6918b97aabc
keywords:
- WIA_IPS_XRES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_XRES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 776c63f2cb7d6be7c520f67fae64f0a0770e2c92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343820"
---
# <a name="wiaipsxres"></a>WIA\_IP\_XRES


WIA\_IP\_XRES プロパティには、水平方向のデバイスの 1 インチあたりのピクセル単位で現在の解像度が含まれています。

## <span id="ddk_wia_ips_xres_si"></span><span id="DDK_WIA_IPS_XRES_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_XRES プロパティ水平方向の解像度を設定します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

デバイスは、値は 1 つだけに設定することができます、作成、WIA\_PROP\_リストの種類と、有効な値を配置します。 このような状況は、1 つの解像度の設定が別の解像度に依存する場合にも適用されます。 (たとえば、垂直方向の解像度に依存できます水平方向の解像度。)

WIA\_IP\_XRES はすべてのイメージの取得が有効な項目と項目の保存されたイメージに必要です。 ストレージ アイテムを使用できなくなります。

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


[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

[**WIA\_IP\_YRES**](wia-ips-yres.md)

 

 






