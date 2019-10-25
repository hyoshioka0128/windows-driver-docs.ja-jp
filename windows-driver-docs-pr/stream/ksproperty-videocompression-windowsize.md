---
title: KSK プロパティ\_VIDEOCOMPRESSION\_WINDOWSIZE
description: KSK プロパティ\_VIDEOCOMPRESSION\_WINDOWSIZE プロパティは、平均フレームサイズを示すデータ速度を制御します。 このプロパティを実装する必要があります。
ms.assetid: 44cf4bb6-7ddb-4a72-8a77-7dc390aa8c12
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2d2fd8ad29c110c73ee9240b8ed2600b92caa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837877"
---
# <a name="ksproperty_videocompression_windowsize"></a>KSK プロパティ\_VIDEOCOMPRESSION\_WINDOWSIZE


KSK プロパティ\_VIDEOCOMPRESSION\_WINDOWSIZE プロパティは、平均フレームサイズを示すデータ速度を制御します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocompression_windowsize_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、平均フレームサイズを表すデータ速度を指定する LONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**値**メンバー\_videocompression\_S 構造体は、ウィンドウのサイズを指定します。

このプロパティをサポートするミニドライバーは、 [**ksproperty\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)構造体を\_、KS プロパティの**Capabilities**メンバーで**KS\_CompressionCaps**を設定する必要があります。ミニドライバーのビデオ圧縮機能を取得します。 ミニドライバーで**KS\_CompressionCaps\_CanWindow**フラグが設定されている場合は、プロパティの get と set の両方のサポートを提供する必要があります。

サイズが*n*のウィンドウの場合、連続する*n*フレームの平均フレームサイズは、ストリームの指定したデータ速度を超えないようにする必要があります。ただし、*個々*のフレームは、サイズが大きくなったり小さくなったりする可能性があります。 たとえば、データレートが1秒あたり15フレーム (fps) のムービーで150キロバイト/秒 (KBps) に設定されている場合、各フレームの*平均*サイズは 10 kb 以下である必要があります。 個々のフレームは、平均サイズ (ムービーの1秒あたりの15フレームに対して計算される) が 10 kb 以下である限り、サイズが大きくなったり小さくなったりする場合があります。

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

[**KSK プロパティ\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 






