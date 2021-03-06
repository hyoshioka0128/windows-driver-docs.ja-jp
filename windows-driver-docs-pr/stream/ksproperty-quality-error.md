---
title: KSPROPERTY\_品質\_エラー
description: KSPROPERTY\_品質\_エラー プロパティが省略可能なプロパティ、暗証番号 (pin) は、品質管理をサポートしている場合に実装する必要があります。
ms.assetid: a918ef13-f0a7-4eb9-b6ec-dcfec3098c1e
keywords:
- KSPROPERTY_QUALITY_ERROR ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_QUALITY_ERROR
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147599dd0742fbad7ce702af2b35cd479bb428c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361050"
---
# <a name="kspropertyqualityerror"></a>KSPROPERTY\_品質\_エラー


KSPROPERTY\_品質\_エラー プロパティが省略可能なプロパティ、暗証番号 (pin) は、品質管理をサポートしている場合に実装する必要があります。

## <span id="ddk_ksproperty_quality_error_ks"></span><span id="DDK_KSPROPERTY_QUALITY_ERROR_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality)"><strong>KSQUALITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_品質\_エラーは、型のプロパティの値を持つ[ **KSQUALITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality)構造体。 取得または現在使用されているフレームの割合と最適なフレームの受信時刻からデルタを設定するには、この構造体を使用します。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSQUALITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality)

 

 






