---
title: KSPROPERTY\_アロケーター\_コントロール\_HONOR\_数
description: KSPROPERTY\_アロケーター\_コントロール\_HONOR\_COUNT プロパティを割り当てる DirectDraw surface の数を決定する方法をオーバーレイ Mixer に通知します。 このプロパティは省略可能です。
ms.assetid: 3a867554-a6ef-49bd-89e7-e5d09a21609e
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4e27864106eee0627ccae1b1da5ee76eb4d814f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571074"
---
# <a name="kspropertyallocatorcontrolhonorcount"></a>KSPROPERTY\_アロケーター\_コントロール\_HONOR\_数


KSPROPERTY\_アロケーター\_コントロール\_HONOR\_COUNT プロパティを割り当てる DirectDraw surface の数を決定する方法をオーバーレイ Mixer に通知します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_allocator_control_honor_count_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、オーバーレイ Mixer の数を計算し、オーバーレイのサーフェスの使用の方法を指定する DWORD です。

<a name="remarks"></a>コメント
-------

KSPROPERTY\_アロケーター\_コントロール\_HONOR\_カウント プロパティの要求で指定された表面の数を使用してオーバーレイ Mixer を強制的に 1 を返す必要があります、 [ **KSPROPERTY\_接続\_ALLOCATORFRAMING** ](ksproperty-connection-allocatorframing.md)プロパティ。 戻り値が 0 には、割り当てるサーフェスの数を計算するオーバーレイ Mixer が発生します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_接続\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

 

 






