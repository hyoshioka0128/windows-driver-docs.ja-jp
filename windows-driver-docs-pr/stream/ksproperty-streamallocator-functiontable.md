---
title: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE
description: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE プロパティは、特定のアロケーターの関数のテーブルを取得します。
ms.assetid: 5a55c808-2960-41c7-b242-69d1e10d0015
keywords:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99617df4a7971c3a3a4b728ee272586d0c795ba4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368833"
---
# <a name="kspropertystreamallocatorfunctiontable"></a>KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE


KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE プロパティは、特定のアロケーターの関数のテーブルを取得します。

## <span id="ddk_ksproperty_streamallocator_functiontable_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable)"><strong>KSSTREAMALLOCATOR_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE がディスパッチをサポートしているアロケーターによってのみ使用\_LEVEL 関数のインターフェイス。 アロケーターは、このプロパティをサポートできる必要がありますを割り当て、IRQL のディスパッチのフレームを解放\_レベルと低い。 このプロパティは、カーネル モードからのみアクセスできます。

ディスパッチ\_レベルのインターフェイスは密接に関連付けられた IRP ベースのインターフェイスではフレームが返されるときに完了する保留中の I/O を許可する内部通知イベントの作成時に可能性がある関数のテーブルの取得無料のリスト。 アロケーターを識別するハンドルが閉じられたときにテーブルの関数ポインターが有効でないし、関連するイベントが自動的に無効にします。

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


[**KSSTREAMALLOCATOR\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable)

 

 






