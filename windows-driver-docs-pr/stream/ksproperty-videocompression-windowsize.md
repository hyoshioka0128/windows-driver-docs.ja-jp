---
title: KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE
description: KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE プロパティは、平均フレーム サイズを表すデータ速度を制御します。 このプロパティを実装する必要があります。
ms.assetid: 44cf4bb6-7ddb-4a72-8a77-7dc390aa8c12
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE ストリーミング メディア デバイス
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
ms.openlocfilehash: e21e98ae322c3ec27db64ceae9211b7ae6c98002
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529327"
---
# <a name="kspropertyvideocompressionwindowsize"></a>KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE


KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE プロパティは、平均フレーム サイズを表すデータ速度を制御します。 このプロパティを実装する必要があります。

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
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、平均フレーム サイズを表すデータ レートを指定する LONG が。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_構造がウィンドウのサイズを指定します。

このプロパティをサポートするミニドライバーを設定する必要があります、 **KS\_CompressionCaps\_CanWindow**フラグ、**機能**のメンバー、 [ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565979)ミニドライバーのビデオの圧縮機能を取得する構造体。 ミニドライバーが設定されている場合、 **KS\_CompressionCaps\_CanWindow**プロパティの get と set の両方のサポートが提供フラグをします。

サイズのウィンドウの*n、* 連続する任意の平均フレーム サイズ*n*がフレームする必要があります、ストリームの指定されたデータのレートを超えない*個々*フレームを大きくすることがありますまたはより小さい。 たとえば、データ レートが 150 キロバイト/秒 (KBps) の 2 つ目の (fps) 映画ごとに 15 フレームに設定されている場合、*平均*各フレームのサイズは 10 キロバイト未満をするため必要があります。 個々 のフレームは、いれば (映画の 1 秒あたりの間で計算される 15 のフレーム) の平均サイズが 10 キロバイト以下大きくまたは小さくする可能性があります。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566018)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565979)

 

 






