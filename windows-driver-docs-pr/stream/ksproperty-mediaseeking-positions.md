---
title: KSK プロパティ\_MEDIASEEKING\_位置
description: KSK プロパティ\_MEDIASEEKING\_位置プロパティは、メディア時間やフィルターの停止時刻を設定します。
ms.assetid: 20f0e97a-37bb-4c01-8012-b73bb765f4b9
keywords:
- KSPROPERTY_MEDIASEEKING_POSITIONS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_POSITIONS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5d8d2f57f3b670670e0b93b31b042f43030d03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842298"
---
# <a name="ksproperty_mediaseeking_positions"></a>KSK プロパティ\_MEDIASEEKING\_位置


KSK プロパティ\_MEDIASEEKING\_位置プロパティは、メディア時間やフィルターの停止時刻を設定します。

## <span id="ddk_ksproperty_mediaseeking_positions_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_POSITIONS_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions" data-raw-source="[&lt;strong&gt;KSPROPERTY_POSITIONS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions)"><strong>KSPROPERTY_POSITIONS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSK プロパティ\_position 構造体は、ストリームの合計継続時間を基準とした現在位置と停止位置を指定します。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions)

 

 






