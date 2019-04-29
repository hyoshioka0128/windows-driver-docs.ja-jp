---
title: KSPROPERTY\_VPCONFIG\_SCALEFACTOR
description: KSPROPERTY\_VPCONFIG\_SCALEFACTOR プロパティは、ユーザー定義の仕様にビデオ ポート ディメンションを設定します。
ms.assetid: 0fbfedc8-9dff-4c7c-910f-507b84614e47
keywords:
- KSPROPERTY_VPCONFIG_SCALEFACTOR ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SCALEFACTOR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed1e335fe0c3261e10d10b09d0a66e7eac8ce10a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386496"
---
# <a name="kspropertyvpconfigscalefactor"></a>KSPROPERTY\_VPCONFIG\_SCALEFACTOR


KSPROPERTY\_VPCONFIG\_SCALEFACTOR プロパティは、ユーザー定義の仕様にビデオ ポート ディメンションを設定します。

## <span id="ddk_ksproperty_vpconfig_scalefactor_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SCALEFACTOR_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567268" data-raw-source="[&lt;strong&gt;KS_AMVPSIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567268)"><strong>KS_AMVPSIZE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_AMVPSIZE 構造体のビデオ ポートの高さと幅を指定します。

<a name="remarks"></a>注釈
-------

KSPROPSETID でこのプロパティを使用するときに\_VPVBIConfig、プロパティのすべての要求は状態を返す必要があります\_いない\_実装されていません。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KS\_AMVPSIZE**](https://msdn.microsoft.com/library/windows/hardware/ff567268)

 

 






