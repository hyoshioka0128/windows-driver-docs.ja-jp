---
title: KSK プロパティ\_VIDEODECODER\_VCR\_タイミング
description: KSK プロパティ\_VIDEODECODER\_VCR\_タイミングプロパティは、VCR がテープソースまたはブロードキャストソースからのビデオを想定しているかどうかを制御します。 このプロパティは省略可能です。
ms.assetid: 66d194e4-df9e-4f8a-9767-414311c205da
keywords:
- KSPROPERTY_VIDEODECODER_VCR_TIMING ストリーミングメディアデバイス
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
ms.openlocfilehash: baaccbf82a1874fe3d47abdced2f206fb6e3114e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837864"
---
# <a name="ksproperty_videodecoder_vcr_timing"></a>KSK プロパティ\_VIDEODECODER\_VCR\_タイミング


KSK プロパティ\_VIDEODECODER\_VCR\_タイミングプロパティは、VCR がテープソースまたはブロードキャストソースからのビデオを想定しているかどうかを制御します。 このプロパティは省略可能です。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、VCR のタイミングまたはブロードキャストのタイミングを使用するかどうかを指定する ULONG です。 値が0の場合は、ブロードキャストソースが示されます。 0以外の値は、テープのソースを示します。

<a name="remarks"></a>注釈
-------

KSK プロパティの**値**メンバー\_videodecoder\_S 構造体は、VCR のタイミングまたはブロードキャストのタイミングのどちらを使用するかを示します。

通常、テープソースでの同期パルスのタイミングの精度は、ブロードキャストソースの場合ほど正確ではありません。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 






