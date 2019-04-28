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
ms.openlocfilehash: a005a5a85d09ac0fe396ddfc19ab2593af19c12e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380818"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

 

 






