---
title: KSK プロパティ\_PIN\_名
description: クライアントは、KSK プロパティ\_使用して\_名をピン留めして、pin ファクトリのレジストリ名を取得します。 これは、Unicode のローカライズされた文字列です。
ms.assetid: 763c3116-95f5-4d32-8c46-d8d91f537bd4
keywords:
- KSPROPERTY_PIN_NAME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NAME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe858d254f60c478111f6b59024796d1aa0348b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838851"
---
# <a name="ksproperty_pin_name"></a>KSK プロパティ\_PIN\_名


クライアントは、KSK プロパティ\_使用して\_名をピン留めして、pin ファクトリのレジストリ名を取得します。 これは、Unicode のローカライズされた文字列です。

## <span id="ddk_ksproperty_pin_name_ks"></span><span id="DDK_KSPROPERTY_PIN_NAME_KS"></span>


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
<td><p>ローカライズされた Unicode 文字列を格納しているバッファー。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、KSP\_PIN を使用して指定します。この場合、メンバーは、レジストリ名を返す pin ファクトリを指定します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリームクラスドライバーは、ストリーム要求ブロックを使用してこのプロパティを処理し、詳細情報を照会します。

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

 

 






