---
title: KSPROPERTY\_VIDEOPROCAMP\_CONTRAST
description: KSK プロパティ\_VIDEOPROCAMP\_CONTRAST プロパティは、カメラのコントラスト (ルミナンスゲイン) 設定を制御します。 このプロパティは省略可能です。
ms.assetid: 0e94aec4-b258-44be-aa6e-f0a40b803564
keywords:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST ストリーミングメディアデバイス
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
ms.openlocfilehash: 632bfd9f33e820c4dd7d434e23a4a04d3f23b3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844765"
---
# <a name="ksproperty_videoprocamp_contrast"></a>KSPROPERTY\_VIDEOPROCAMP\_CONTRAST


KSK プロパティ\_VIDEOPROCAMP\_CONTRAST プロパティは、カメラのコントラスト (ルミナンスゲイン) 設定を制御します。 このプロパティは省略可能です。

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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラのコントラスト設定を指定する LONG です。 コントラスト値は、100を乗算した利益率として表されます。

<a name="remarks"></a>注釈
-------

VIDEOPROCAMP\_S 構造体\_KSK プロパティの**値**メンバーは、コントラスト値を指定します。

すべてのビデオキャプチャミニドライバーで、このプロパティの**value**メンバーの範囲と既定値を定義する必要があります。 必要な範囲は 0 ~ 1万でなければなりません。 既定値は 100 (1x) である必要があります。

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

[**KSK プロパティ\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






