---
title: KSPROPERTY\_PIN\_GLOBALCINSTANCES
description: クライアントの使用、KSPROPERTY\_PIN\_このピンの工場出荷時の pin の最大数と同様に、暗証番号 (pin) ファクトリによってインスタンス化ピンの現在の数を決定する GLOBALCINSTANCES をインスタンス化できます。 このプロパティは省略可能です。
ms.assetid: 888b8ddf-aa36-4e2f-a74c-ab4ee693bb36
keywords:
- KSPROPERTY_PIN_GLOBALCINSTANCES ストリーミング メディア デバイス
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
ms.openlocfilehash: f23ee0e85078b007897d5925dcf73829efd08be9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361096"
---
# <a name="kspropertypinglobalcinstances"></a>KSPROPERTY\_PIN\_GLOBALCINSTANCES


クライアントの使用、KSPROPERTY\_PIN\_このピンの工場出荷時の pin の最大数と同様に、暗証番号 (pin) ファクトリによってインスタンス化ピンの現在の数を決定する GLOBALCINSTANCES をインスタンス化できます。 このプロパティは省略可能です。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、場所、 **PinId**メンバーが、ピン留めするファクトリを指定します。

KSPIN\_CINSTANCES はフォームのデータ構造体。

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

次に、KSPIN の各メンバーの説明\_CINSTANCES 構造体。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
ドライバー、または KSINTANCE にピン留めする、ピン留めするファクトリをインスタンス化の最大数を指定します\_中間状態の最大値がない場合。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
ドライバーの pin の pin のファクトリがインスタンス化の現在の数を指定します。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

KSPROPERTY\_PIN\_GLOBALCINSTANCES フィルターのすべてのインスタンスに対するインスタンスの絶対と現在の最大数を指定します。 フィルターごとの値を調べるには[ **KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

 

 






