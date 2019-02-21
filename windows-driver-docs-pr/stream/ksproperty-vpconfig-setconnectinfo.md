---
title: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO
description: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO プロパティは、ユーザー定義の接続情報を持つビデオ ポートの構成を設定します。 DDVIDEOPORTCONNECT 構造体の配列へのポインターである、KSPROPERTY によって返される\_VPCONFIG\_GETCONNECTINFO プロパティ。
ms.assetid: 120f6889-cd67-4c05-b4b8-adab3efd7f2c
keywords:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21146c1a74f064b582037e6154c258c40923139d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530668"
---
# <a name="kspropertyvpconfigsetconnectinfo"></a>KSPROPERTY\_VPCONFIG\_SETCONNECTINFO


KSPROPERTY\_VPCONFIG\_SETCONNECTINFO プロパティは、ユーザー定義の接続情報を持つビデオ ポートの構成を設定します。 配列へのポインターが[ **DDVIDEOPORTCONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff550388)構造体を KSPROPERTY によって返されると\_VPCONFIG\_GETCONNECTINFO プロパティ。

## <span id="ddk_ksproperty_vpconfig_setconnectinfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETCONNECTINFO_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550388" data-raw-source="[&lt;strong&gt;DDVIDEOPORTCONNECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550388)"><strong>DDVIDEOPORTCONNECT</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ビデオ ポート接続の構成を記述する DDVIDEOPORTCONNECT 構造です。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DDVIDEOPORTCONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff550388)

[**KSPROPERTY\_VPCONFIG\_GETCONNECTINFO**](ksproperty-vpconfig-getconnectinfo.md)

 

 






