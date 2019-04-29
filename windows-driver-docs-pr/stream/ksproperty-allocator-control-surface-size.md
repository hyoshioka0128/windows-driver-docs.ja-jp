---
title: KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ
description: KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ プロパティは、キャプチャ操作が進行状況とすること (オーバーレイ Mixer) など、DirectDraw surface アロケーターを提供するフィルターをクライアントに通知オーバーレイの現在のサイズに関係なく固定サイズでは、Microsoft DirectDraw サーフェスを割り当てる必要があります。 このプロパティは省略可能です。
ms.assetid: fc759013-9dd7-44fc-a0d7-fd2585975966
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a5d70a547c742132e99baa553d4f6b26292349b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384153"
---
# <a name="kspropertyallocatorcontrolsurfacesize"></a>KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ


KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ プロパティは、キャプチャ操作が進行状況とすること (オーバーレイ Mixer) など、DirectDraw surface アロケーターを提供するフィルターをクライアントに通知オーバーレイの現在のサイズに関係なく固定サイズでは、Microsoft DirectDraw サーフェスを割り当てる必要があります。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_allocator_control_surface_size_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564280" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564280)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S</strong></a></p></td>
<td><p>ULONGs のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、1 組の幅を指定する ULONGs とオーバーレイ サーフェスの高さが。

<a name="remarks"></a>注釈
-------

このプロパティをサポートするミニドライバーは、KSPROPERTY を返す\_アロケーター\_コントロール\_画面\_サイズ\_幅と高さのオーバーレイが必要なサーフェスを記述する S 構造体。 オーバーレイ Mixer では、このサイズのオーバーレイのサーフェスを割り当てます。 暗証番号 (pin) の接続中に、メディアの種類で指定されたサイズでない場合、ビデオはビデオ ポートではこのサイズに拡大縮小します。 その他のビデオ ポートでのスケーリングは行われません、VGA チップのスケーリング能力に関係なく。

ミキサーがその主な入力ピンのビデオ ポートを使用してこのプロパティのアップ ストリーム フィルターに接続されている場合、オーバーレイ Mixer は常にこの新しいプロパティを照会します。 そのフィルターがこのプロパティを実装していない場合、オーバーレイ Mixer でデータをキャプチャしていないととして正しく表示されるビデオを保持するために必要なビデオ ポートにビデオを拡大または縮小します。

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

[**KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564280)

 

 






