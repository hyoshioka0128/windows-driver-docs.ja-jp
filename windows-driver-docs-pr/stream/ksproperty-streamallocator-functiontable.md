---
title: KSK プロパティ\_STREAMALLOCATOR\_FUNCTIONTABLE
description: '\_STREAMALLOCATOR\_FUNCTIONTABLE プロパティは、指定されたアロケーターの関数テーブルを取得します。'
ms.assetid: 5a55c808-2960-41c7-b242-69d1e10d0015
keywords:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE ストリーミングメディアデバイス
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
ms.openlocfilehash: 9f99eb9b155abd0e597f38485ed675a565574863
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837935"
---
# <a name="ksproperty_streamallocator_functiontable"></a>KSK プロパティ\_STREAMALLOCATOR\_FUNCTIONTABLE


\_STREAMALLOCATOR\_FUNCTIONTABLE プロパティは、指定されたアロケーターの関数テーブルを取得します。

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
<td><p>アロケーター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)"><strong>KSSTREAMALLOCATOR_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSK プロパティ\_STREAMALLOCATOR\_FUNCTIONTABLE は、ディスパッチ\_LEVEL 関数インターフェイスをサポートするアロケーターによってのみ使用されます。 このプロパティをサポートするアロケーターは、ディスパッチ\_レベル以下の IRQL に対して、フレームの割り当てと解放を行うことができる必要があります。 このプロパティは、カーネルモードからのみアクセスできます。

ディスパッチ\_レベルのインターフェイスは、IRP ベースのインターフェイスと密接に関連付けられているため、関数テーブルを取得すると、内部通知イベントが生成され、フレームがに返されたときに、保留中の i/o を完了できるようになります。無料の一覧。 アロケーターへのハンドルが閉じられると、関数テーブルのポインターは無効になり、関連付けられているイベントは自動的に無効になります。

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


[**KSSTREAMALLOCATOR\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)

 

 






