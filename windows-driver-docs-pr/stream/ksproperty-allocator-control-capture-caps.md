---
title: KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_キャップ
description: '\_コントロール\_\_CAPTURE プロパティ\_アロケータープロパティは、ビデオポートのキャプチャ機能をオーバーレイミキサーに通知します (キャプチャのサポートが利用可能な場合)。'
ms.assetid: 9e2947a3-ef5b-4a2a-a607-6c0c4be44b1c
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dcc23d0fb622bcde3b32c69b2a38012523e2456
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832010"
---
# <a name="ksproperty_allocator_control_capture_caps"></a>KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_キャップ


\_コントロール\_\_CAPTURE プロパティ\_アロケータープロパティは、ビデオポートのキャプチャ機能をオーバーレイミキサーに通知します (キャプチャのサポートが利用可能な場合)。

## <span id="ddk_ksproperty_allocator_control_capture_caps_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONG で、インターリーブキャプチャがサポートされているかどうかを指定します。

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

[**KSK プロパティ\_アロケーター\_コントロール\_キャプチャ\_キャップ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s)

 

 






