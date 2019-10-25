---
title: KSK プロパティ\_ストリーム\_のプレゼンテーションエクステント
description: クライアントは、ストリームエクステントのクエリを実行するために、KSK プロパティ\_ストリーム\_のプレゼンテーションエクステント要求を送信します。
ms.assetid: 36b66035-f935-4264-8555-d949865d708e
keywords:
- KSPROPERTY_STREAM_PRESENTATIONEXTENT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_PRESENTATIONEXTENT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7f985f152e51be68e0d4dfc091b1d6d2516255
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837947"
---
# <a name="ksproperty_stream_presentationextent"></a>KSK プロパティ\_ストリーム\_のプレゼンテーションエクステント


クライアントは、ストリームエクステントのクエリを実行するために、KSK プロパティ\_ストリーム\_のプレゼンテーションエクステント要求を送信します。

## <span id="ddk_ksproperty_stream_presentationextent_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONEXTENT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティは、プレゼンテーション時間と同じ解像度形式で、長さを LONGLONG として返します。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






