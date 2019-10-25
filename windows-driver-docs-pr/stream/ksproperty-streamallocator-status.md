---
title: KSK プロパティ\_STREAMALLOCATOR\_状態
description: KSK プロパティ\_STREAMALLOCATOR\_STATUS プロパティは、指定されたアロケーターの現在の状態を取得します。
ms.assetid: af88253b-e72d-4ea9-855d-0a91e6e35d0f
keywords:
- KSPROPERTY_STREAMALLOCATOR_STATUS ストリーミングメディアデバイス
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
ms.openlocfilehash: e0b448619923a9f09c3c3a603dca1432cc269916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837933"
---
# <a name="ksproperty_streamallocator_status"></a>KSK プロパティ\_STREAMALLOCATOR\_状態


KSK プロパティ\_STREAMALLOCATOR\_STATUS プロパティは、指定されたアロケーターの現在の状態を取得します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)"><strong>KSSTREAMALLOCATOR_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

アロケーターの状態は、フレーミングの仕様と現在割り当てられているフレームを示します。

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


[**KSSTREAMALLOCATOR の\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)

 

 






