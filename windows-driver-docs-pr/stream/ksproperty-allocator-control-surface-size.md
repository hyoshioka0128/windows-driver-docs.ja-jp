---
title: KSK プロパティ\_アロケーター\_コントロール\_サーフェイス\_サイズ
description: '\_アロケータープロパティ\_CONTROL\_SURFACE\_SIZE プロパティは、キャプチャ操作が進行中であること、および Microsoft DirectDraw が実行中であることを示す DirectDraw SURFACE アロケーター (オーバーレイミキサーなど) を提供するクライアントフィルターに通知します。サーフェイスは、オーバーレイの現在のサイズに関係なく、固定サイズで割り当てる必要があります。 このプロパティは省略可能です。'
ms.assetid: fc759013-9dd7-44fc-a0d7-fd2585975966
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE ストリーミングメディアデバイス
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
ms.openlocfilehash: ec8f3001e3c09a185323ff663d7912f8fab011bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832002"
---
# <a name="ksproperty_allocator_control_surface_size"></a>KSK プロパティ\_アロケーター\_コントロール\_サーフェイス\_サイズ


\_アロケータープロパティ\_CONTROL\_SURFACE\_SIZE プロパティは、キャプチャ操作が進行中であること、および Microsoft DirectDraw が実行中であることを示す DirectDraw SURFACE アロケーター (オーバーレイミキサーなど) を提供するクライアントフィルターに通知します。サーフェイスは、オーバーレイの現在のサイズに関係なく、固定サイズで割り当てる必要があります。 このプロパティは省略可能です。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S</strong></a></p></td>
<td><p>ULONGs のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、オーバーレイサーフェスの幅と高さを指定する ULONGs のペアです。

<a name="remarks"></a>注釈
-------

このプロパティをサポートするミニドライバーは、必要なオーバーレイサーフェイスの幅と高さを記述する\_コントロール\_\_\_SURFACE プロパティ\_アロケーターを返します。 オーバーレイミキサーは、このサイズのオーバーレイサーフェスを割り当てます。 Pin 接続中に MediaType で指定されたサイズでない場合、ビデオはビデオポートでこのサイズにスケーリングされます。 VGA チップのスケーリング機能に関係なく、ビデオポートでのその他のスケーリングは発生しません。

オーバーレイミキサーは、ミキサーがプライマリ入力ピンのビデオポートを介してこのプロパティの上流フィルターに接続されている場合、常にこの新しいプロパティを照会します。 このフィルターでこのプロパティが実装されていない場合、オーバーレイミキサーは、ビデオが正しく表示されるように、必要に応じてビデオポートでビデオのサイズを調整します。

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

[**KSK プロパティ\_アロケーター\_コントロール\_サーフェイス\_サイズ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)

 

 






