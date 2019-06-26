---
title: KSPROPERTY\_EXTXPORT\_MEDIUM\_情報
description: KSPROPERTY\_EXTXPORT\_MEDIUM\_情報プロパティは、外部のデバイスのメディアに関する情報を取得します。
ms.assetid: 04b98c50-ebb0-4224-b476-d261b7c5dd79
keywords:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f708586880b3d761c2ba6e4e30c4d3ffd4cac9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354846"
---
# <a name="kspropertyextxportmediuminfo"></a>KSPROPERTY\_EXTXPORT\_MEDIUM\_情報


KSPROPERTY\_EXTXPORT\_MEDIUM\_情報プロパティは、外部のデバイスのメディアに関する情報を取得します。

## <span id="ddk_ksproperty_extxport_medium_info_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_MEDIUM_INFO_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-medium_info" data-raw-source="[&lt;strong&gt;MEDIUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-medium_info)"><strong>MEDIUM_INFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、メディア\_外部デバイスにメディアを記述する情報の構造体が読み込まれます。 、カセット テープなどは、テープのグレードと、書き込み保護。

<a name="remarks"></a>注釈
-------

**MediumInfo** 、KSPROPERTY のメンバー\_EXTXPORT\_構造情報を指定します。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**MEDIUM\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-medium_info)

 

 






