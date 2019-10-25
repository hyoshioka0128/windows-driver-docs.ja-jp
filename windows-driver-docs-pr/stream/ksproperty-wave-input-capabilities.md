---
title: KSK プロパティ\_WAVE\_入力\_機能
description: KSK プロパティ\_WAVE\_入力\_機能プロパティは、wave デバイスの入力機能を返します。
ms.assetid: 84ed0f41-52b6-40e0-b334-c336e158cbfc
keywords:
- KSPROPERTY_WAVE_INPUT_CAPABILITIES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_INPUT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45dbd960e6bb94371fea3d16683234c25ee6e699
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845369"
---
# <a name="ksproperty_wave_input_capabilities"></a>KSK プロパティ\_WAVE\_入力\_機能


KSK プロパティ\_WAVE\_入力\_機能プロパティは、wave デバイスの入力機能を返します。

## <span id="ddk_ksproperty_wave_input_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_INPUT_CAPABILITIES_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities" data-raw-source="[&lt;strong&gt;KSWAVE_INPUT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities)"><strong>KSWAVE_INPUT_CAPABILITIES</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、wave デバイスの入力機能を記述する KSWAVE\_入力\_機能構造です。これには、オーディオチャネルの最大数、サンプルあたりのビット数、サンプリング頻度の範囲などが含まれます。接続の合計とアクティブな数が表示されます。

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

[**KSWAVE\_入力\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities)

 

 






