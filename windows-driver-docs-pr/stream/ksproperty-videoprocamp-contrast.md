---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_コントラスト
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_コントラスト プロパティは、カメラのコントラスト (ルミナンス利益) の設定を制御します。 このプロパティは省略可能です。
ms.assetid: 0e94aec4-b258-44be-aa6e-f0a40b803564
keywords:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20cff4112d147d423a1a9f2bc71892edb33c2529
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381959"
---
# <a name="kspropertyvideoprocampcontrast"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_コントラスト


KSPROPERTY\_ビデオ プロシージャ アンプ\_コントラスト プロパティは、カメラのコントラスト (ルミナンス利益) の設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_contrast_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_CONTRAST_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラのコントラスト設定を指定する LONG が。 コントラスト値は 100 倍向上要素として表されます。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_の構造は、コントラスト値を指定します。

すべてのビデオ キャプチャ ミニドライバーの範囲と既定値を定義する必要があります、**値**このプロパティのメンバー。 必要な範囲は 0 ~ 10000 である必要があります。 既定値は 100 (1 x) である必要があります。

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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






