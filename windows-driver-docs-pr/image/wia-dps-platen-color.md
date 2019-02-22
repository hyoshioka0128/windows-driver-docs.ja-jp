---
title: WIA\_DPS\_プラテン\_色
description: WIA\_DPS\_プラテン\_色プロパティにはからプラテン上の現在の色が含まれています。
ms.assetid: d1bc9bc8-ad23-48b8-8456-21aa3556ab69
keywords:
- WIA_DPS_PLATEN_COLOR イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PLATEN_COLOR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613b8448d2b5364a4c0059256ab49165b573f68d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560589"
---
# <a name="wiadpsplatencolor"></a>WIA\_DPS\_プラテン\_色


WIA\_DPS\_プラテン\_色プロパティにはからプラテン上の現在の色が含まれています。

## <span id="ddk_wia_dps_platen_color_si"></span><span id="DDK_WIA_DPS_PLATEN_COLOR_SI"></span>


プロパティの種類:VT\_UI1 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

ミニドライバーは、WIA を報告する必要があります\_DPS\_プラテン\_(これは、Microsoft Windows SDK ドキュメントで説明されている) RGBQUAD 構造体の形式で 4 バイト値のベクターとしての色。 WIA ミニドライバーは、作成し、このプロパティを保持します。

アプリケーションは、WIA を読み取ります\_DPS\_プラテン\_色スキャナーからプラテン上の色を取得します。 この色は、処理後の最終的なイメージのアプリケーションに役立ちます。

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

 

 





