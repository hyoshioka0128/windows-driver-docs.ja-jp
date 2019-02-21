---
title: WIA\_DPS\_パッド\_色
description: WIA\_DPS\_パッド\_WIA ミニドライバーにアラインされていないデータが埋められるときに使用される現在の周囲の色がカラー プロパティに含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: db78fc1b-72e4-4edc-8f4f-9209e6b36aa6
keywords:
- WIA_DPS_PAD_COLOR イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAD_COLOR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45da42ad8c6d7d70794a31c49e9d3ea44d79beca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559465"
---
# <a name="wiadpspadcolor"></a>WIA\_DPS\_パッド\_色


WIA\_DPS\_パッド\_WIA ミニドライバーにアラインされていないデータが埋められるときに使用される現在の周囲の色がカラー プロパティに含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dps_pad_color_si"></span><span id="DDK_WIA_DPS_PAD_COLOR_SI"></span>


プロパティの種類:VT\_UI1 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_DPS\_パッド\_色プロパティは、(これは、Microsoft Windows SDK ドキュメントで説明されている) RGBQUAD 構造体の形式で 4 バイト値のベクターとして報告する必要があります。

アプリケーションは、WIA を読み取ります\_DPS\_パッド\_の色を使用するパディングの色を取得します。

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

 

 





