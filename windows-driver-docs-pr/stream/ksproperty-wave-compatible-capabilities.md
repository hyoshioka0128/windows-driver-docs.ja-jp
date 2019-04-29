---
title: KSPROPERTY\_WAVE\_互換性のある\_機能
description: KSPROPERTY\_WAVE\_互換性のある\_機能プロパティは、デバイスの波の互換性のある機能を決定します。
ms.assetid: 59b24d84-8b98-4928-aaae-46cb14c0d140
keywords:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7377393d7df9c1c927d719083447a20b36be0865
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329974"
---
# <a name="kspropertywavecompatiblecapabilities"></a>KSPROPERTY\_WAVE\_互換性のある\_機能


KSPROPERTY\_WAVE\_互換性のある\_機能プロパティは、デバイスの波の互換性のある機能を決定します。

## <span id="ddk_ksproperty_wave_compatible_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567242" data-raw-source="[&lt;strong&gt;KSWAVE_COMPATCAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567242)"><strong>KSWAVE_COMPATCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSWAVE\_wave デバイスは、入力を受け付ける場合について説明します COMPATCAPS 構造の出力は、または両方します。

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

[**KSWAVE\_COMPATCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff567242)

 

 






