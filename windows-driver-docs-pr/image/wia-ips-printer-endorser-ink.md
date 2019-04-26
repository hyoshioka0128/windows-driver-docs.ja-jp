---
title: WIA\_IP\_プリンター\_裏書き\_インク
description: WIA\_IP\_プリンター\_裏書き\_・ インプリント ・裏書き/デバイスの現在のインクまたはトナーの状態をレポートにインクのプロパティを使用します。
ms.assetid: CCD7C10A-7739-4E75-B30C-2C2E7FE90B13
keywords:
- WIA_IPS_PRINTER_ENDORSER_INK イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_INK
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00dcd70369a07020ad8fefe18436f8e42642578
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351162"
---
# <a name="wiaipsprinterendorserink"></a>WIA\_IP\_プリンター\_裏書き\_インク


**WIA\_IP\_プリンター\_裏書き\_インク**・ インプリント ・裏書き/デバイスの現在のインクまたはトナーの状態を報告するプロパティを使用します。 プロパティの値では、合計容量に対して占める割合として残りの利用可能なインクを示します。 たとえば、値 50 が半分または 50% のインクの残量を示します。 このプロパティは初期化され、WIA ミニ ドライバーによって維持されます。 この機能は、Windows 8 および Windows の以降のバージョンで使用できます。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

**WIA\_IP\_プリンター\_裏書き\_インク**プロパティは・ インプリント ・/裏書き項目のオプションです。 このプロパティの有効な値は、0 から 100 までの間は。

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

 

 





