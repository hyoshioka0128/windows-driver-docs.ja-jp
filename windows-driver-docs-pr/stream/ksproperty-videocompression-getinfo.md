---
title: KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO
description: KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO プロパティは、デバイスのビデオ圧縮機能を取得します。 このプロパティを実装する必要があります。
ms.assetid: 87e19e19-d90e-49c6-a6f0-cf33abf28c01
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_GETINFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_GETINFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6278172647b8bdf5a829acbb9ced7ff96a6b0295
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837887"
---
# <a name="ksproperty_videocompression_getinfo"></a>KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO


KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO プロパティは、デバイスのビデオ圧縮機能を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocompression_getinfo_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_GETINFO_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、VIDEOCOMPRESSION\_GETINFO\_S 構造\_、圧縮機能をクエリするストリームなどのビデオ圧縮設定を指定する、既定のキーフレームレート、既定の予測フレームレート、既定の品質設定、品質設定の数、およびさまざまな圧縮機能。

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

[**KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 






