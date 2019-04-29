---
title: KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO
description: KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO プロパティは、デバイスのビデオの圧縮機能を取得します。 このプロパティを実装する必要があります。
ms.assetid: 87e19e19-d90e-49c6-a6f0-cf33abf28c01
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_GETINFO ストリーミング メディア デバイス
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
ms.openlocfilehash: cb2fe8a164623b0b496e47d452d05adea7a5c569
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385178"
---
# <a name="kspropertyvideocompressiongetinfo"></a>KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO


KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO プロパティは、デバイスのビデオの圧縮機能を取得します。 このプロパティを実装する必要があります。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565979" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565979)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565979" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565979)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_構造をストリームの圧縮機能を持つはクエリを実行するには、既定のキーなどのビデオの圧縮設定を指定します。フレーム レートは、既定値は、フレーム レート、品質の既定の設定、品質の設定の数、およびさまざまな圧縮機能を予測します。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565979)

 

 






