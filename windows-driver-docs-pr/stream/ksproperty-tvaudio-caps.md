---
title: KSK プロパティ\_TVAUDIO\_CAPS
description: KSK プロパティ\_TVAUDIO\_CAPS プロパティは、テレビオーディオデバイスの機能を取得します。 このプロパティを実装する必要があります。
ms.assetid: a5b7348e-0f85-430c-acf0-c35e289ef338
keywords:
- KSPROPERTY_TVAUDIO_CAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ee38b6e80d76308c750cd60a04cc9bef1b37185
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837893"
---
# <a name="ksproperty_tvaudio_caps"></a>KSK プロパティ\_TVAUDIO\_CAPS


KSK プロパティ\_TVAUDIO\_CAPS プロパティは、テレビオーディオデバイスの機能を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_caps_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)"><strong>KSPROPERTY_TVAUDIO_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ステレオと mono オーディオのサポートや複数の言語機能など、テレビオーディオデバイスの機能を指定する ULONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**capabilities**メンバー\_TVAUDIO\_CAPS\_S 構造体は、テレビオーディオデバイスの機能を指定します。

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

[**KSK プロパティ\_TVAUDIO\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)

 

 






