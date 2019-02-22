---
title: WIA\_IPA\_平面
description: WIA\_IPA\_平面プロパティにはオプションの梱包イメージ データが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: df4013db-8f9e-428a-83dd-c344f7998034
keywords:
- WIA_IPA_PLANAR イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_PLANAR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e3708de0cb31754ea19340cbc5a05cbf1a83f27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528411"
---
# <a name="wiaipaplanar"></a>WIA\_IPA\_平面


WIA\_IPA\_平面プロパティにはオプションの梱包イメージ データが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_planar_si"></span><span id="DDK_WIA_IPA_PLANAR_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_リストまたは WIA\_PROP\_NONE

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

アプリケーションは、WIA を読み取ります\_IPA\_平面画像パッキング オプションまたはパッキング オプションの現在のイメージを設定を確認します。

次の表に、WIA で有効な定数\_IPA\_平面。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PACKED_PIXEL</p></td>
<td><p>イメージ データがパック ピクセル形式です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PLANAR</p></td>
<td><p>イメージ データが平面の形式です。</p></td>
</tr>
</tbody>
</table>

 

WIA を実装することができる場合、デバイスは、値は 1 つだけに設定することができます、\_IPA\_平面のプロパティとして WIA\_PROP\_NONE および読み取り専用です。

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで廃止します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





