---
title: KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT
description: KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT プロパティがサポートされているピクセル形式の配列を取得します。
ms.assetid: 74cc8cbc-cd81-43e1-ba15-3105a4c70808
keywords:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cebe2ec4848c532d5f131268bad594b32847851
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573862"
---
# <a name="kspropertyvpconfiggetvideoformat"></a>KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT


KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT プロパティがサポートされているピクセル形式の配列を取得します。

## <span id="ddk_ksproperty_vpconfig_getvideoformat_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_GETVIDEOFORMAT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550274" data-raw-source="[&lt;strong&gt;DDPIXELFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550274)"><strong>DDPIXELFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ビデオのポートのピクセル形式を説明する DDPIXELFORMAT 構造です。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)

 

 






