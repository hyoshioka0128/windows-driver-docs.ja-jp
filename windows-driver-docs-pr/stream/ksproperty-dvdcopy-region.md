---
title: KSPROPERTY\_DVDCOPY\_リージョン
description: KSPROPERTY\_DVDCOPY\_REGION プロパティは、言語の制限に従って DVD コピー防止の領域を指定します。
ms.assetid: b0ad355b-607f-43c5-9959-a309c6c63259
keywords:
- KSPROPERTY_DVDCOPY_REGION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_REGION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53aea7985010841a83d0447ef7cb073ba4c5b018
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580085"
---
# <a name="kspropertydvdcopyregion"></a>KSPROPERTY\_DVDCOPY\_リージョン


KSPROPERTY\_DVDCOPY\_REGION プロパティは、言語の制限に従って DVD コピー防止の領域を指定します。

## <span id="ddk_ksproperty_dvdcopy_region_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_REGION_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567638" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567638)"><strong>KS_DVDCOPY_REGION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_国籍または言語の地域コードを記述する領域の構造。

<a name="remarks"></a>コメント
-------

言語の制限の詳細については、次を参照してください。 [DVD 加入](https://msdn.microsoft.com/library/windows/hardware/ff559512)と[DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KS\_DVDCOPY\_REGION**](https://msdn.microsoft.com/library/windows/hardware/ff567638)

 

 






