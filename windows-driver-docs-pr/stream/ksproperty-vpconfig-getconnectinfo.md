---
title: KSPROPERTY\_VPCONFIG\_GETCONNECTINFO
description: KSPROPERTY\_VPCONFIG\_GETCONNECTINFO プロパティは、すべての可能なビデオ ポート構成を取得します。
ms.assetid: 30ac1f7d-0218-49ed-8f6d-e58f56aee70e
keywords:
- KSPROPERTY_VPCONFIG_GETCONNECTINFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_GETCONNECTINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 174a9dc6794eb1a972ee333fd0567670e5d95e5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531741"
---
# <a name="kspropertyvpconfiggetconnectinfo"></a>KSPROPERTY\_VPCONFIG\_GETCONNECTINFO


KSPROPERTY\_VPCONFIG\_GETCONNECTINFO プロパティは、すべての可能なビデオ ポート構成を取得します。

## <span id="ddk_ksproperty_vpconfig_getconnectinfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_GETCONNECTINFO_KS"></span>


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
<td><p>〇</p></td>
<td><p>X</p></td>
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

 

 






