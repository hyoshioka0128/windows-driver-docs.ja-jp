---
title: KSK プロパティ\_ピン\_カテゴリ
description: クライアントは、KSK プロパティ\_ピン留め\_CATEGORY プロパティを使用して、pin ファクトリのカテゴリを取得します。
ms.assetid: 6579408c-9ec5-4b09-9a63-815cec5bd5a3
keywords:
- KSPROPERTY_PIN_CATEGORY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CATEGORY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f6dcf6053f24a2abe02d6c264635c312e104ffe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842754"
---
# <a name="ksproperty_pin_category"></a>KSK プロパティ\_ピン\_カテゴリ


クライアントは、KSK プロパティ\_ピン留め\_CATEGORY プロパティを使用して、pin ファクトリのカテゴリを取得します。

## <span id="ddk_ksproperty_pin_category_ks"></span><span id="DDK_KSPROPERTY_PIN_CATEGORY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP\_ピン構造の**Pinid**メンバーは、カテゴリ GUID を返すピンファクトリを指定します。

KS フィルターは、このプロパティを使用して、ピンファクトリによってインスタンス化されるピンの標準の機能*カテゴリ*を示します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。stream クラスドライバーは、必要に応じて詳細情報を照会するストリーム要求ブロックを使用して、このプロパティを処理します。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






