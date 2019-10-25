---
title: KSK プロパティ\_VIDEOCONTROL\_フレーム\_レート
description: KSK プロパティ\_VIDEOCONTROL\_FRAME\_率プロパティは、使用可能なフレームレートを列挙します。 このプロパティは省略可能です。
ms.assetid: f2b6fabc-c03b-4fa5-9e5b-43d7a1c26578
keywords:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES ストリーミングメディアデバイス
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
ms.openlocfilehash: 319d5dec3856aadd69eef5ae84d78a495737e503
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837873"
---
# <a name="ksproperty_videocontrol_frame_rates"></a>KSK プロパティ\_VIDEOCONTROL\_フレーム\_レート


KSK プロパティ\_VIDEOCONTROL\_FRAME\_率プロパティは、使用可能なフレームレートを列挙します。 このプロパティは省略可能です。

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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、100ナノ秒単位で使用可能なフレームレートを示す KSMULTIPLE\_ITEM 配列です。

<a name="remarks"></a>注釈
-------

使用可能なフレームレートは、KSMULTIPLE\_ITEM 配列に返されます。 アプリケーションは、ミニドライバー a KSK プロパティ\_VIDEOCONTROL\_フレーム\_レート要求を送信します。この要求は、KSK プロパティのストリームインデックスとイメージのサイズを指定し\_VIDEOCONTROL\_FRAME\_率\_S 構造体を指定します。 ミニドライバーは、呼び出し元の KSMULTIPLE\_ITEM 配列バッファーのフレームレート情報を返します。 このバッファーには固定ヘッダー (KSMULTIPLE\_ITEM) と、その後に続く可変長のデータ (KSK MULTIPLE\_ITEM 構造の値に基づく) があります。

個々の値は、100 nansecond 単位で指定します。

ミニドライバーに渡されたバッファーのサイズが0の場合、ミニドライバーは、ミニドライバーに渡される要求\_ブロック構造体を、必要なバッファーのサイズに\_\_設定して、に渡すように、**に渡し**ます。バッファー\_オーバーフロー\_状態を返します。

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

[**KSK プロパティ\_VIDEOCONTROL\_フレーム\_レート\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)

 

 






