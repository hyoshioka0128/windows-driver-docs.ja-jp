---
title: KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY
description: KSK プロパティ\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY プロパティは、ローカルの電源線の頻度を指定します。 デバイスで、蛍光灯環境のアンチフリッカー処理がサポートされている場合は、頻度が必要になることがあります。
ms.assetid: 560bb16d-2a95-408f-b32c-fa2db1c94902
keywords:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86462f270ef5a0454199aa968bb70c1cf0b18d99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845225"
---
# <a name="ksproperty_videoprocamp_powerline_frequency"></a>KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY


KSK プロパティ\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY プロパティは、ローカルの電源線の頻度を指定します。 デバイスで、蛍光灯環境のアンチフリッカー処理がサポートされている場合は、頻度が必要になることがあります。

## <span id="ddk_ksproperty_videoprocamp_powerline_frequency_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY_KS"></span>


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

 

プロパティ値 (操作データ) は、ローカルの電力線の頻度を指定する LONG です。 値は、カメラの現在の電源ライン設定を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>電源ライン周波数コントロールが無効になっています。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>電力線の周波数は 50 Hz です。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>電力線の周波数は 60 Hz です。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>電力線の頻度は、システムによって自動的に決定されます。</p>
<div class="alert">すべてのカメラ (UVC 1.1) では、自動プロパティ値 (3) を使用できない  に
<strong>注意</strong>してください。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントは、set 要求を行うときに、前の表の値のいずれかを\_VIDEOPROCAMP\_NODE\_S 構造体の KSK プロパティの**値**のメンバーに指定する必要があります。

Get 要求を行うと、クライアントは、前の表の値のいずれかを、\_VIDEOPROCAMP\_NODE\_S 構造体の KSK プロパティの**値**メンバーで受け取ります。

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

[**PowerlineFrequency 列挙型**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.PowerlineFrequency)

 

 






