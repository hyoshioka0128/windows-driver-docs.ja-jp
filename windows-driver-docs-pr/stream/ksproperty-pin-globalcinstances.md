---
title: KSK プロパティ\_\_GLOBALCINSTANCES にピン留めする
description: クライアントは、KSK プロパティを使用して\_GLOBALCINSTANCES\_ピン留めして、ピンファクトリによってインスタンス化された現在の pin の数と、このピンファクトリがインスタンス化できる pin の最大数を決定します。 このプロパティは省略可能です。
ms.assetid: 888b8ddf-aa36-4e2f-a74c-ab4ee693bb36
keywords:
- KSPROPERTY_PIN_GLOBALCINSTANCES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_GLOBALCINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1c95334a1a667caf9c089a028c7d98c96d3a65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838855"
---
# <a name="ksproperty_pin_globalcinstances"></a>KSK プロパティ\_\_GLOBALCINSTANCES にピン留めする


クライアントは、KSK プロパティを使用して\_GLOBALCINSTANCES\_ピン留めして、ピンファクトリによってインスタンス化された現在の pin の数と、このピンファクトリがインスタンス化できる pin の最大数を決定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_pin_globalcinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_GLOBALCINSTANCES_KS"></span>


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
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、KSP\_PIN を使用して指定します。 **Pinid**メンバーは、pin ファクトリを指定します。

KSPIN\_CINSTANCES は、次の形式のデータ構造です。

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

KSPIN\_CINSTANCES 構造体の各メンバーの説明を次に示します。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
Pin ファクトリがドライバーでインスタンス化できる pin の最大数を指定します。最大数を指定しない場合は、KSK が\_不確定であることを示します。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
Pin ファクトリがドライバーでインスタンス化した現在の pin の数を指定します。

クラスドライバーは、このプロパティを処理しません。stream ミニドライバーは、独自の処理を提供する必要があります。

KSK プロパティ\_ピン\_GLOBALCINSTANCES は、フィルターのすべてのインスタンスについて、現在および最大のインスタンス数を指定します。 フィルターごとの値を決定するには、 [**Ksk プロパティ\_使用して\_CINSTANCES にピン留め**](ksproperty-pin-cinstances.md)します。

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

[**KSK プロパティ\_ピン\_CINSTANCES**](ksproperty-pin-cinstances.md)

 

 






