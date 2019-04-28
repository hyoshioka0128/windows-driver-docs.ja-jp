---
title: KSPROPERTY\_DROPPEDFRAMES\_現在
description: KSPROPERTY\_ドロップ\_フレーム\_CURRENT プロパティは、キャプチャしたフレームの数、平均フレームのサイズと削除すると、フレームの数を動的にビデオ キャプチャ ミニドライバーを取得します。 このプロパティを実装する必要があります。
ms.assetid: 43367858-4e3b-476e-aaa5-c9e665df8dc6
keywords:
- KSPROPERTY_DROPPEDFRAMES_CURRENT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DROPPEDFRAMES_CURRENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f39c780b1c308cd0af5fe093f692f59d08078da7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380640"
---
# <a name="kspropertydroppedframescurrent"></a>KSPROPERTY\_DROPPEDFRAMES\_現在


KSPROPERTY\_ドロップ\_フレーム\_CURRENT プロパティは、キャプチャしたフレームの数、平均フレームのサイズと削除すると、フレームの数を動的にビデオ キャプチャ ミニドライバーを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_droppedframes_current_ks"></span><span id="DDK_KSPROPERTY_DROPPEDFRAMES_CURRENT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565138" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565138)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565138" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565138)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_DROPPEDFRAMES\_現在\_構造を現在の画像の数、フレームのドロップの数とキャプチャされたフレームの平均サイズを指定します。

<a name="remarks"></a>注釈
-------

キャプチャされたフレームの欠落したフレームの数には、ストリームの状態が遷移停止を一時停止するときをリセットする必要があります。

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

[**KSPROPERTY\_DROPPEDFRAMES\_現在\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565138)

 

 






