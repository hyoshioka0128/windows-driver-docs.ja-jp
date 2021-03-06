---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_POWERLINE\_頻度
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_POWERLINE\_頻度プロパティは、地域の電力線の数を指定します。 頻度をデバイスは、蛍光灯環境対策ちらつきの処理をサポートしている場合に必要なことがあります。
ms.assetid: 560bb16d-2a95-408f-b32c-fa2db1c94902
keywords:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10332d104e7da15be931f16887a254da65a7a539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381925"
---
# <a name="kspropertyvideoprocamppowerlinefrequency"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_POWERLINE\_頻度


KSPROPERTY\_ビデオ プロシージャ アンプ\_POWERLINE\_頻度プロパティは、地域の電力線の数を指定します。 頻度をデバイスは、蛍光灯環境対策ちらつきの処理をサポートしている場合に必要なことがあります。

## <span id="ddk_ksproperty_videoprocamp_powerline_frequency_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY_KS"></span>


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

 

プロパティの値 (データの操作) は、地域の電力線の数を指定する LONG が。 値は、カメラの現在の電力線の設定を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>電力線の頻度のコントロールが無効です。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>電力線の頻度が 50 Hz できます。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>電力線の頻度が 60 Hz できます。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>電力線の頻度は、システムによって自動的に決定されます。</p>
<div class="alert">
<strong>注</strong>  自動プロパティの値 (3) がすべてのカメラの使用可能な (UVC 1.1 具体的には)。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントがで上記の表に、値のいずれかを指定する必要がありますセット要求を行うときに、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

Get 要求を行うときに、クライアントは受信値のいずれかで上記の表に、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

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

[**PowerlineFrequency 列挙型**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.PowerlineFrequency)

 

 






