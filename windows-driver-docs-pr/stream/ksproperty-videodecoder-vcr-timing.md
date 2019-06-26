---
title: KSPROPERTY\_VIDEODECODER\_VCR\_タイミング
description: KSPROPERTY\_VIDEODECODER\_VCR\_プロパティ コントロールのタイミング、VCR はテープ ソースまたはブロードキャストのソースからのビデオを予期しているかどうか。 このプロパティは省略可能です。
ms.assetid: 66d194e4-df9e-4f8a-9767-414311c205da
keywords:
- KSPROPERTY_VIDEODECODER_VCR_TIMING ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_VCR_TIMING
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 311467778422992f90a46820c37d54227babce8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381969"
---
# <a name="kspropertyvideodecodervcrtiming"></a>KSPROPERTY\_VIDEODECODER\_VCR\_タイミング


KSPROPERTY\_VIDEODECODER\_VCR\_プロパティ コントロールのタイミング、VCR はテープ ソースまたはブロードキャストのソースからのビデオを予期しているかどうか。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videodecoder_vcr_timing_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_VCR_TIMING_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、VCR タイミングを使用して、またはタイミングをブロードキャストするかどうかを指定する ULONG です。 ゼロの値では、ブロードキャストのソースを示します。 0 以外の値では、テープのソースを示します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEODECODER\_構造が VCR のタイミングを使用して、またはタイミングをブロードキャストするかどうかを示します。

通常のテープのソースで同期パルス タイミング精度はブロードキャストのソースから正確ではありません。

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

[**KSPROPERTY\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 






