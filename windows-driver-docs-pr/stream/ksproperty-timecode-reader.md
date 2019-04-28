---
title: KSPROPERTY\_タイムコード\_リーダー
description: KSPROPERTY\_タイムコード\_リーダー プロパティを現在のテープの位置のタイムコードを取得します。
ms.assetid: 16029ac8-5de0-4d8c-9a48-549dbea29ae7
keywords:
- KSPROPERTY_TIMECODE_READER ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TIMECODE_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd96b9dcb708218c4985a77dd743a1fe98d2585b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363976"
---
# <a name="kspropertytimecodereader"></a>KSPROPERTY\_タイムコード\_リーダー


KSPROPERTY\_タイムコード\_リーダー プロパティを現在のテープの位置のタイムコードを取得します。

## <span id="ddk_ksproperty_timecode_reader_ks"></span><span id="DDK_KSPROPERTY_TIMECODE_READER_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565781" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565781)"><strong>KSPROPERTY_TIMECODE_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568528" data-raw-source="[&lt;strong&gt;TIMECODE_SAMPLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568528)"><strong>TIMECODE_SAMPLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) はタイムコード\_テープの現在位置のタイムコードを示すサンプル構造体。

<a name="remarks"></a>注釈
-------

**TimecodeSamp** 、KSPROPERTY のメンバー\_タイムコード\_の構造は、現在のテープの位置のタイムコードをについて説明します。

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

[**KSPROPERTY\_タイムコード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565781)

[**タイムコード\_サンプル**](https://msdn.microsoft.com/library/windows/hardware/ff568528)

 

 






