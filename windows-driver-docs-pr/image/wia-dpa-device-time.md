---
title: WIA\_DPA\_デバイス\_時間
description: WIA\_DPA\_デバイス\_時のプロパティには、デバイスに格納されている現在の時刻が含まれています。 ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 5f903eb8-6a9e-4f06-ba70-5c02d8b332e5
keywords:
- WIA_DPA_DEVICE_TIME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPA_DEVICE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba4df830b50bebf7b832799734dcff4c7fed6424
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391110"
---
# <a name="wiadpadevicetime"></a>WIA\_DPA\_デバイス\_時間


WIA\_DPA\_デバイス\_時のプロパティには、デバイスに格納されている現在の時刻が含まれています。 ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dpa_device_time_si"></span><span id="DDK_WIA_DPA_DEVICE_TIME_SI"></span>


プロパティの種類:VT\_UI2 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込みまたは読み取り専用

<a name="remarks"></a>注釈
-------

ときに、WIA\_DPA\_デバイス\_時のプロパティは読み取り専用で、ミニドライバーは、デバイスの現在の時刻を確認する必要があり、現在の時刻を常に返す必要があります。 このプロパティは、内部のクロックのデバイスでのみサポートされます。 デバイスの時計を設定できますが場合、このプロパティは、読み取り/書き込みです。それ以外の場合、読み取り専用です。 WIA デバイスは、(これは、Microsoft Windows SDK ドキュメントで説明されている)、SYSTEMTIME 構造体の時間を報告します。

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

 

 





