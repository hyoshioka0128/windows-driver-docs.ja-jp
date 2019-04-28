---
title: KSPROPERTY\_DVDSUBPIC\_HLI
description: KSPROPERTY\_DVDSUBPIC\_HLI プロパティは、色やコントラストなどのサブピクチャまたは画面を変更する四角形を指定します。
ms.assetid: c3498ff8-11fe-4f53-8317-83a487684ac7
keywords:
- KSPROPERTY_DVDSUBPIC_HLI ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_HLI
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c43354af2ddf72cba864ec1fa2e7e575f50d1e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377448"
---
# <a name="kspropertydvdsubpichli"></a>KSPROPERTY\_DVDSUBPIC\_HLI


KSPROPERTY\_DVDSUBPIC\_HLI プロパティは、色やコントラストなどのサブピクチャまたは画面を変更する四角形を指定します。

## <span id="ddk_ksproperty_dvdsubpic_hli_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_HLI_KS"></span>


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
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565627" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPHLI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565627)"><strong>KSPROPERTY_SPHLI</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_SPHLI 構造体、DVD を変更する情報を強調表示します。

<a name="remarks"></a>注釈
-------

[ **KSPROPERTY\_SPHLI** ](https://msdn.microsoft.com/library/windows/hardware/ff565627)構造が DVD の強調表示情報から現在選択されているボタンについて説明します。

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


[**KSPROPERTY\_SPHLI**](https://msdn.microsoft.com/library/windows/hardware/ff565627)

 

 






