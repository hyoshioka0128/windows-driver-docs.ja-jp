---
title: KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_インターリーブ
description: KSK プロパティ\_アロケーター\_コントロール\_\_CAPTURE プロパティは、インターリーブキャプチャが可能な場合にオーバーレイミキサーに通知します。
ms.assetid: ea38289f-2d4e-4613-ba08-c8ab49f6fce7
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f90750744062dc0de3b7f112f44fa773701977a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832007"
---
# <a name="ksproperty_allocator_control_capture_interleave"></a>KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_インターリーブ


KSK プロパティ\_アロケーター\_コントロール\_\_CAPTURE プロパティは、インターリーブキャプチャが可能な場合にオーバーレイミキサーに通知します。

## <span id="ddk_ksproperty_allocator_control_capture_interleave_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、インターリーブキャプチャが可能かどうかを指定する ULONG です。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_インターリーブ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)

 

 






