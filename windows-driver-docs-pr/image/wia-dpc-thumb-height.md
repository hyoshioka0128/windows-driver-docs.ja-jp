---
title: WIA\_DPC\_THUMB\_高さ
description: WIA\_DPC\_THUMB\_HEIGHT プロパティには、新しくキャプチャしたイメージを使用するサムネイル イメージのピクセル単位で高さを定義します。
ms.assetid: bc4ad063-7287-461e-a31b-d4b6628372b6
keywords:
- WIA_DPC_THUMB_HEIGHT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_THUMB_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6343cd5da28df70ca5c65163e3ac53d483e298d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392559"
---
# <a name="wiadpcthumbheight"></a>WIA\_DPC\_THUMB\_高さ


WIA\_DPC\_THUMB\_HEIGHT プロパティには、新しくキャプチャしたイメージを使用するサムネイル イメージのピクセル単位で高さを定義します。

## <span id="ddk_wia_dpc_thumb_height_si"></span><span id="DDK_WIA_DPC_THUMB_HEIGHT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE または WIA\_PROP\_一覧

アクセス権:読み取り専用または読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPC\_THUMB\_ユーザー インターフェイスでサムネイル画像を表示するための推定サイズを取得する高さの値。

場合、値または WIA\_DPC\_THUMB\_の高さは、WIA\_PROP\_、アクセス権があります読み取り専用。 値は、WIA 場合\_PROP\_一覧で、アクセス権は読み取り/書き込みである必要があります。

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
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPC\_THUMB\_幅**](wia-dpc-thumb-width.md)

 

 






