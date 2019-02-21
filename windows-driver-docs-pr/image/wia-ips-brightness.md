---
title: WIA\_IP\_明るさ
description: WIA\_IP\_BRIGHTNESS プロパティには、デバイスの現在のハードウェアの明るさの設定が含まれています。
ms.assetid: 3954cf52-3bb1-4b76-9ff4-a638e1ddde83
keywords:
- WIA_IPS_BRIGHTNESS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BRIGHTNESS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcb6d628f90ced00b536eabb3ead2add23f47f20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530437"
---
# <a name="wiaipsbrightness"></a>WIA\_IP\_明るさ


WIA\_IP\_BRIGHTNESS プロパティには、デバイスの現在のハードウェアの明るさの設定が含まれています。

## <span id="ddk_wia_ips_brightness_si"></span><span id="DDK_WIA_IPS_BRIGHTNESS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_明るさプロパティをハードウェアの明るさの値にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。

Wia 値\_IP\_−1000 場所最大輝度に対応する 1000、0 に対応する通常の明るさ、および −1000 に対応する最小の明度の 1000 の範囲で明るさをマップする必要があります。

WIA\_IP\_のすべてのイメージの取得項目は、明るさが必要です。

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

 

 





