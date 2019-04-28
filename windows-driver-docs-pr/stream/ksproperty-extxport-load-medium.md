---
title: KSPROPERTY\_EXTXPORT\_ロード\_中
description: KSPROPERTY\_EXTXPORT\_読み込む\_中程度のプロパティを設定または外部のデバイスの読み込み中に取得します。 例を取り出し、トレイ、閉じるトレイなどを開きます。
ms.assetid: 13ec61ae-4be7-4af6-875f-a6ca178cf6bc
keywords:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0795737987f6e7eba87096b63ac328fe9669a8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380821"
---
# <a name="kspropertyextxportloadmedium"></a>KSPROPERTY\_EXTXPORT\_ロード\_中


KSPROPERTY\_EXTXPORT\_読み込む\_中程度のプロパティを設定または外部のデバイスの読み込み中に取得します。 例を取り出し、トレイ、閉じるトレイなどを開きます。

## <span id="ddk_ksproperty_extxport_load_medium_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_LOAD_MEDIUM_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565167" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565167)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、現在の読み込み中を指定する ULONG です。 たとえば取り出し、トレイまたは閉じたトレイを開きます。

<a name="remarks"></a>注釈
-------

**LoadMedium** 、KSPROPERTY のメンバー\_EXTXPORT\_構造がロード メディアを指定します。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)

 

 






