---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_明るさ
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_BRIGHTNESS プロパティは、明るさの設定を制御します。 このプロパティは省略可能です。
ms.assetid: 8b099ff1-e64a-4723-9834-8a42450bebd4
keywords:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c0eadda61dcd7c94a235e9757678ec2c9ad5b54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582541"
---
# <a name="kspropertyvideoprocampbrightness"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_明るさ


KSPROPERTY\_ビデオ プロシージャ アンプ\_BRIGHTNESS プロパティは、明るさの設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_brightness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS_KS"></span>


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
<td><p>はい</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの明るさの設定を指定する LONG が。 この値は、NTSC ソースの 100 倍して切る単位で表されます。 NTSC 以外のソースでは、ユニットと非表示を表す 0 から 10000 の純粋な空白を表す任意、です。

<a name="remarks"></a>コメント
-------

**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_S 構造体を明るさを指定します。

明るさは、黒のレベルとも呼ばれます。 明るさの設定を変更するすべての輝度値に対して均等に全体のビデオ信号を移動します。

すべてのビデオ キャプチャ ミニドライバーには、このプロパティの値を範囲と既定値を定義する必要があります。 必要な範囲は +10000 を-10000 である必要があります。 既定値は 750 (7.5 切る) である必要があります。

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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 






