---
title: KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金
description: KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金プロパティが使用可能なフレーム レートを列挙します。 このプロパティは省略可能です。
ms.assetid: f2b6fabc-c03b-4fa5-9e5b-43d7a1c26578
keywords:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfec663015f615077acea8bdac8f2c8a886864ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355927"
---
# <a name="kspropertyvideocontrolframerates"></a>KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金


KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金プロパティが使用可能なフレーム レートを列挙します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videocontrol_frame_rates_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_FRAME_RATES_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong> </a>配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSMULTIPLE\_を 100 ナノ秒単位で使用可能なフレーム レートを記述する項目の配列。

<a name="remarks"></a>注釈
-------

使用可能なフレーム レートが、KSMULTIPLE で返される\_アイテムの配列。 アプリケーションに送信、ミニドライバーを KSPROPERTY\_VIDEOCONTROL\_フレーム\_、KSPROPERTY でストリームのインデックスとイメージのサイズを指定するレート要求\_VIDEOCONTROL\_フレーム\_料金\_S 構造体。 ミニドライバーは、呼び出し元の KSMULTIPLE でフレーム レート情報を返します\_項目配列バッファー。 このバッファーは固定ヘッダー (KSMULTIPLE\_項目)、およびそれに続くデータの可変長の量 (、KSMULTIPLE の値に基づいて\_項目の構造)。

個々 の値では、100 nansecond 単位です。

バッファーのサイズが渡された場合、ミニドライバーは、0、ようにミニドライバーに設定する必要があります、 **NumberOfBytesToTransfer**ハードウェア ベースのメンバー\_ストリーム\_要求\_に渡されるブロック構造、ミニドライバー バッファーのサイズが必要なし、状態を返す\_バッファー\_オーバーフローが発生します。

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

[**KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)

 

 






