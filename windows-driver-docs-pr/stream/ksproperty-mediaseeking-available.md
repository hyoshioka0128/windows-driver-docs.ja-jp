---
title: KSPROPERTY\_MEDIASEEKING\_利用可能
description: KSPROPERTY\_MEDIASEEKING\_利用可能なプロパティをフィルターで現在利用可能なメディアの期間を取得します。
ms.assetid: df59f32e-2783-418d-85b9-f9285034c6fa
keywords:
- KSPROPERTY_MEDIASEEKING_AVAILABLE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_AVAILABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe35e182fc0d7c3d31d0c7bd630a7d8c91026b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366110"
---
# <a name="kspropertymediaseekingavailable"></a>KSPROPERTY\_MEDIASEEKING\_利用可能


KSPROPERTY\_MEDIASEEKING\_利用可能なプロパティをフィルターで現在利用可能なメディアの期間を取得します。

## <span id="ddk_ksproperty_mediaseeking_available_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_AVAILABLE_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565178" data-raw-source="[&lt;strong&gt;KSPROPERTY_MEDIAAVAILABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565178)"><strong>KSPROPERTY_MEDIAAVAILABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

メディアの有効期間は、期間をクライアントがシークできます。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_MEDIAAVAILABLE**](https://msdn.microsoft.com/library/windows/hardware/ff565178)

[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






