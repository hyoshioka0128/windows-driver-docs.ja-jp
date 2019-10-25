---
title: KSK プロパティ\_VIDEOPROCAMP\_バックライト\_補正
description: KSK プロパティ\_VIDEOPROCAMP\_バックライト\_補正プロパティは、カメラのバックライト補正設定を制御します。 このプロパティは省略可能です。
ms.assetid: d893fc01-048a-4f2e-8587-d71be0796dcc
keywords:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86f4f2131a3f23febdee16db88d508e90b0486e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837862"
---
# <a name="ksproperty_videoprocamp_backlight_compensation"></a>KSK プロパティ\_VIDEOPROCAMP\_バックライト\_補正


KSK プロパティ\_VIDEOPROCAMP\_バックライト\_補正プロパティは、カメラのバックライト補正設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_backlight_compensation_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION_KS"></span>


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

 

プロパティ値 (操作データ) は、カメラのバックライト補正設定を指定する LONG です。 この値には、0または1を指定できます。 このプロパティの既定値は1です。 値0は、バックライト補正が無効であることを示します。 既定値の1は、バックライト補正が有効になっていることを示します。

<a name="remarks"></a>注釈
-------

VIDEOPROCAMP\_S 構造体\_KSK プロパティの**値**メンバーは、バックライト補正が有効か無効かを指定します。

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

 

 






