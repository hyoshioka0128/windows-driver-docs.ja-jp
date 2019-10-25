---
title: KSK プロパティ\_TVAUDIO\_現在使用可能な\_モード\_
description: 現在\_使用可能な\_モードプロパティの KSK プロパティ\_TVAUDIO\_は、デバイスで使用可能なテレビオーディオモードを取得します。 このプロパティを実装する必要があります。
ms.assetid: 9c98771a-7a41-469d-a441-da5c1ac5a697
keywords:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d6bd4ecda077a30a9f08184f90713247394ce7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837896"
---
# <a name="ksproperty_tvaudio_currently_available_modes"></a>KSK プロパティ\_TVAUDIO\_現在使用可能な\_モード\_


現在\_使用可能な\_モードプロパティの KSK プロパティ\_TVAUDIO\_は、デバイスで使用可能なテレビオーディオモードを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_currently_available_modes_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、現在利用可能なテレビオーディオモード (ステレオや mono オーディオ、複数言語設定など) を指定する ULONG です。

<a name="remarks"></a>注釈
-------

TVAUDIO\_S 構造体\_KSK プロパティの**モード**メンバーは、オーディオモードを指定します。 このメソッドには、情報の要求時にデバイスでサポートされているモードを示す、KS\_TVAUDIO\_MODE\_\* フラグのビットごとの or 演算が含まれています。

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

 

 






