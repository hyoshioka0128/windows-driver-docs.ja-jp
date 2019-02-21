---
title: WIA\_DPS\_垂直\_ベッド\_登録
description: WIA\_DPS\_垂直\_ベッド\_REGISTRATION プロパティには、登録、または垂直方向の配置および境界の検出、スキャナーのベッドに配置されているドキュメントが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 58c1bfb2-1f61-4910-ac6d-189aa203c370
keywords:
- WIA_DPS_VERTICAL_BED_REGISTRATION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_VERTICAL_BED_REGISTRATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9173ac0a275817e31af6060b6a52c4417d33c885
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531755"
---
# <a name="wiadpsverticalbedregistration"></a>WIA\_DPS\_垂直\_ベッド\_登録


WIA\_DPS\_垂直\_ベッド\_REGISTRATION プロパティには、登録、または垂直方向の配置および境界の検出、スキャナーのベッドに配置されているドキュメントが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dps_vertical_bed_registration_si"></span><span id="DDK_WIA_DPS_VERTICAL_BED_REGISTRATION_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_DPS\_垂直\_ベッド\_プロパティを登録します。

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
<td><p>BOTTOM_JUSTIFIED</p></td>
<td><p>このペーパーでは、下端揃えです。</p></td>
</tr>
<tr class="even">
<td><p>中央揃え</p></td>
<td><p>用紙が中央に配置します。</p></td>
</tr>
<tr class="odd">
<td><p>TOP_JUSTIFIED</p></td>
<td><p>このペーパーでは、上部に揃えて配置します。</p></td>
</tr>
</tbody>
</table>

 

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


[**WIA\_DPS\_水平\_ベッド\_登録**](wia-dps-horizontal-bed-registration.md)

 

 






