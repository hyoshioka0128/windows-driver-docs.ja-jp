---
title: KSK プロパティ\_TVAUDIO\_モード
description: KSK プロパティ\_TVAUDIO\_MODE プロパティは、デバイスのオーディオモードを設定します。 このプロパティを実装する必要があります。
ms.assetid: ef2db4b9-307f-4f70-8c9f-1344420c8cba
keywords:
- KSPROPERTY_TVAUDIO_MODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4915954b56e08fb94d3d9371544245e7a4e16e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837891"
---
# <a name="ksproperty_tvaudio_mode"></a>KSK プロパティ\_TVAUDIO\_モード


KSK プロパティ\_TVAUDIO\_MODE プロパティは、デバイスのオーディオモードを設定します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_mode_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_MODE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ステレオや mono のオーディオと言語の設定など、現在の TV オーディオモードを指定する ULONG です。

<a name="remarks"></a>注釈
-------

TVAUDIO\_S 構造体\_KSK プロパティの**モード**メンバーは、オーディオモードを指定します。

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

[**KSK プロパティ\_TVAUDIO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)

 

 






