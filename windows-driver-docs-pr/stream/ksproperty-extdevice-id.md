---
title: KSK プロパティ\_EXTDEVICE\_ID
description: KSK プロパティ\_EXTDEVICE\_ID プロパティは、外部デバイスの汎用システム全体の Id を取得します。
ms.assetid: ff0f37f8-55a8-45b9-8cf1-81e2cc5ac3aa
keywords:
- KSPROPERTY_EXTDEVICE_ID ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_ID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0992004c619088921974b2a7c4653b63b85f4939
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827030"
---
# <a name="ksproperty_extdevice_id"></a>KSK プロパティ\_EXTDEVICE\_ID


KSK プロパティ\_EXTDEVICE\_ID プロパティは、外部デバイスの汎用システム全体の Id を取得します。

## <span id="ddk_ksproperty_extdevice_id_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_ID_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>DWORD 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、外部デバイスの一意のノード Id を指定する DWORD 配列です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**Nodeuniqueid**メンバー\_extdevice\_S 構造体は、外部デバイスの一意のノード Id を指定します。

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

[**KSK プロパティ\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

 






