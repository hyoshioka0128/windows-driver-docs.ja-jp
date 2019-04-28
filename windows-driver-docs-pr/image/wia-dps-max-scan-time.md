---
title: WIA\_DPS\_最大\_スキャン\_時間
description: WIA\_DPS\_最大\_スキャン\_プロパティ時間には (ミリ秒単位)、現在のプロパティ設定で 1 つのページをスキャンする最大時間が含まれています。
ms.assetid: 28c24b1b-9318-46d2-86eb-f948247de8ab
keywords:
- WIA_DPS_MAX_SCAN_TIME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_MAX_SCAN_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8dcd940aa7b479399ff08b6d50366cdcbf8a514
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375836"
---
# <a name="wiadpsmaxscantime"></a>WIA\_DPS\_最大\_スキャン\_時間


WIA\_DPS\_最大\_スキャン\_プロパティ時間には (ミリ秒単位)、現在のプロパティ設定で 1 つのページをスキャンする最大時間が含まれています。

## <span id="ddk_wia_dps_max_scan_time_si"></span><span id="DDK_WIA_DPS_MAX_SCAN_TIME_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPS\_最大\_スキャン\_時間プロパティ ページをスキャンにかかる時間を推定量をします。 この見積もりは、応答しなくなったデバイスの条件を決定する場合に便利です。 WIA ミニドライバーは、作成し、このプロパティを保持します。

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

 

 





