---
title: KSPROPERTY\_WAVE\_バッファー
description: KSPROPERTY\_WAVE\_バッファー プロパティには、wave デバイスのバッファーがについて説明します。
ms.assetid: b2ef458a-a701-4403-875b-1b06164c80a1
keywords:
- KSPROPERTY_WAVE_BUFFER ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_BUFFER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6703261497045fb2dc4854bea9ee063bd4e049
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578428"
---
# <a name="kspropertywavebuffer"></a>KSPROPERTY\_WAVE\_バッファー


KSPROPERTY\_WAVE\_バッファー プロパティには、wave デバイスのバッファーがについて説明します。

## <span id="ddk_ksproperty_wave_buffer_ks"></span><span id="DDK_KSPROPERTY_WAVE_BUFFER_KS"></span>


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
<td><p>はい</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567239" data-raw-source="[&lt;strong&gt;KSWAVE_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567239)"><strong>KSWAVE_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSWAVE\_バッファー、バッファー サイズ (バイト単位)、およびバッファーの開始アドレスの属性をループを記述するバッファーの構造体。

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

[**KSWAVE\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff567239)

 

 






