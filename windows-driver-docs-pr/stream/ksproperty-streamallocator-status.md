---
title: KSPROPERTY\_STREAMALLOCATOR\_状態
description: KSPROPERTY\_STREAMALLOCATOR\_STATUS プロパティを指定したアロケーターの現在の状態を取得します。
ms.assetid: af88253b-e72d-4ea9-855d-0a91e6e35d0f
keywords:
- KSPROPERTY_STREAMALLOCATOR_STATUS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAMALLOCATOR_STATUS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b13cf9fdb22ad1fcd141f868120de3939967875
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363988"
---
# <a name="kspropertystreamallocatorstatus"></a>KSPROPERTY\_STREAMALLOCATOR\_状態


KSPROPERTY\_STREAMALLOCATOR\_STATUS プロパティを指定したアロケーターの現在の状態を取得します。

## <span id="ddk_ksproperty_streamallocator_status_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_STATUS_KS"></span>


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
<td><p>アロケーター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566866" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566866)"><strong>KSSTREAMALLOCATOR_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

アロケーターの状態は、フレームの仕様と現在割り当てられているフレームを示します。

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


[**KSSTREAMALLOCATOR\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566866)

 

 






