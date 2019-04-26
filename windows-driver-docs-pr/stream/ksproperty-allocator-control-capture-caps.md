---
title: KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_キャップ
description: KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_CAPS プロパティ (つまりのキャプチャのサポートが利用可能なかどうか) のビデオ ポートのキャプチャ機能のオーバーレイ Mixer に通知します。
ms.assetid: 9e2947a3-ef5b-4a2a-a607-6c0c4be44b1c
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS ストリーミング メディア デバイス
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
ms.openlocfilehash: 5d1ce8036545de2526ec0bd0cd0679b74b290d10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354501"
---
# <a name="kspropertyallocatorcontrolcapturecaps"></a>KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_キャップ


KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_CAPS プロパティ (つまりのキャプチャのサポートが利用可能なかどうか) のビデオ ポートのキャプチャ機能のオーバーレイ Mixer に通知します。

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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564269" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564269)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ULONG、インターリーブのキャプチャはサポートされているかどうかを指定します。

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

[**KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564269)

 

 






