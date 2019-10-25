---
title: KSK プロパティ\_EXTXPORT\_状態
description: KSK プロパティ\_EXTXPORT\_STATE プロパティは、外部デバイスのトランスポートモードと状態を設定または取得します。
ms.assetid: c508b6ce-2a37-4fca-9edf-66700d9cbd15
keywords:
- KSPROPERTY_EXTXPORT_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cebb63463dc7c3c93c5d9ceae0f64aa0f8899d65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838053"
---
# <a name="ksproperty_extxport_state"></a>KSK プロパティ\_EXTXPORT\_状態


KSK プロパティ\_EXTXPORT\_STATE プロパティは、外部デバイスのトランスポートモードと状態を設定または取得します。

## <span id="ddk_ksproperty_extxport_state_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state" data-raw-source="[&lt;strong&gt;TRANSPORT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)"><strong>TRANSPORT_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、外部トランスポートの現在のモードと状態を記述するトランスポート\_状態構造体です。 たとえば、モードが play に設定されている場合は、状態が freeze (一時停止) に設定されている可能性があります。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_EXTXPORT\_S 構造体の**XPrtState**メンバーは、モードと状態を指定します。

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

[**KSK プロパティ\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**トランスポートの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)

 

 






