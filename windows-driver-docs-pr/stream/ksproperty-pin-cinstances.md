---
title: KSK プロパティ\_ピン\_CINSTANCES
description: このピンファクトリがインスタンス化したピンの現在の数、およびこのピンファクトリがインスタンス化できるピンの最大数 (フィルターあたり)。
ms.assetid: 0a6c0afa-1bdf-4b80-a8d7-55f13d9da74b
keywords:
- KSPROPERTY_PIN_CINSTANCES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94923f1b641b5cf9d038c05a580e20622bf6b85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842748"
---
# <a name="ksproperty_pin_cinstances"></a>KSK プロパティ\_ピン\_CINSTANCES


このピンファクトリがインスタンス化したピンの現在の数、およびこのピンファクトリがインスタンス化できるピンの最大数 (フィルターあたり)。

## <span id="ddk_ksproperty_pin_cinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_CINSTANCES_KS"></span>


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

このプロパティは、KSPIN\_CINSTANCES 型の構造体を返します。

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

KSPIN\_CINSTANCES 構造体の各メンバーの説明を次に示します。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
ピンファクトリがフィルターでインスタンス化できるピンの最大数を指定します。最大数を指定しない場合は、KSK が\_不確定であることを示します。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
ピンファクトリがフィルターでインスタンス化した現在の pin の数を指定します。

このプロパティは、特定のピンファクトリのフィルターごとの最大値を指定します。 指定した pin ファクトリの全体の最大値を指定するには、 [**Ksk プロパティ\_\_GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)プロパティを使用します。

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

 

 





