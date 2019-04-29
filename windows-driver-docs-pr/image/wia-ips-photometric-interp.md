---
title: WIA\_IP\_PHOTOMETRIC\_INTERP
description: WIA\_IP\_PHOTOMETRIC\_INTERP プロパティには白と黒のピクセルの現在の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 5d48ec37-68bb-446a-9236-c88d26f8a549
keywords:
- WIA_IPS_PHOTOMETRIC_INTERP イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PHOTOMETRIC_INTERP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef34df6b44809f83bd295604f7161d9122b49bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383686"
---
# <a name="wiaipsphotometricinterp"></a>WIA\_IP\_PHOTOMETRIC\_INTERP


WIA\_IP\_PHOTOMETRIC\_INTERP プロパティには白と黒のピクセルの現在の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_photometric_interp_si"></span><span id="DDK_WIA_IPS_PHOTOMETRIC_INTERP_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_IP\_PHOTOMETRIC\_INTERP プロパティ (どのようなアプリケーションの実行) に応じて、白または黒のピクセルに割り当てられている値を決定します。

次の表に、WIA で有効な定数\_IP\_PHOTOMETRIC\_INTERP.

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
<td><p>WIA_PHOTO_WHITE_0</p></td>
<td><p>白は 0 です。 と黒の 1 です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PHOTO_WHITE_1</p></td>
<td><p>白は 1 であり、ブラックは 0。</p></td>
</tr>
</tbody>
</table>

 

デバイスは、値は 1 つだけに設定することができます、作成、WIA\_PROP\_リストの種類、および有効な値を配置します。

WIA\_IP\_PHOTOMETRIC\_INTERP プロパティは、すべてのイメージの取得項目と保存された画像に対して必要です。

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

 

 





