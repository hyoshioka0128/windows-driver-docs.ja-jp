---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数\_制限
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数\_LIMIT プロパティをイメージに適用できるデジタル ズーム量上限を指定します。
ms.assetid: 66cc1dd5-3e07-47d8-bb30-b64b90b07ad9
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7d919c9f04e93b41d97a26b56b219539095dc2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381953"
---
# <a name="kspropertyvideoprocampdigitalmultiplierlimit"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数\_制限


KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数\_LIMIT プロパティをイメージに適用できるデジタル ズーム量上限を指定します。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_limit_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの上のデジタル乗数の制限を指定する LONG が。 値は、デバイスは光ディスク イメージに適用可能なデジタル乗数の最大値を指定します。

<a name="remarks"></a>注釈
-------

クライアントがデジタル乗数値を指定する必要がありますセット要求を行うときに、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

クライアントは、デジタルのズームのユーザー定義の上限値を確立するためにセットの要求を使用する場合があります。

クライアントが受信では、前述の値のいずれかで get 要求を行うときに、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






