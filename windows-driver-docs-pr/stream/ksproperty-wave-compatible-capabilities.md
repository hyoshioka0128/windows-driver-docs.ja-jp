---
title: KSK プロパティ\_WAVE\_互換性のある\_機能
description: KSK プロパティ\_WAVE\_互換性のある\_機能プロパティは、デバイスの wave と互換性のある機能を決定します。
ms.assetid: 59b24d84-8b98-4928-aaae-46cb14c0d140
keywords:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 298737768a9be6f69c8c2db895a482b17ccdedad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823598"
---
# <a name="ksproperty_wave_compatible_capabilities"></a>KSK プロパティ\_WAVE\_互換性のある\_機能


KSK プロパティ\_WAVE\_互換性のある\_機能プロパティは、デバイスの wave と互換性のある機能を決定します。

## <span id="ddk_ksproperty_wave_compatible_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps" data-raw-source="[&lt;strong&gt;KSWAVE_COMPATCAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps)"><strong>KSWAVE_COMPATCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、wave デバイスが入力を受け入れるか、出力を生成するか、両方とも実行するかを示す KSWAVE\_COMPATCAPS 構造体です。

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

[**KSWAVE\_COMPATCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_compatcaps)

 

 






