---
title: KSPROPERTY\_PIN\_CINSTANCES
description: この pin ファクトリがインスタンス化、ピンの現在の数だけでなくピン フィルターごとこの pin ファクトリがインスタンスの最大数。
ms.assetid: 0a6c0afa-1bdf-4b80-a8d7-55f13d9da74b
keywords:
- KSPROPERTY_PIN_CINSTANCES ストリーミング メディア デバイス
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
ms.openlocfilehash: 8de2f8a114283deaae9f92581c91c3dae13c5a1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346468"
---
# <a name="kspropertypincinstances"></a>KSPROPERTY\_PIN\_CINSTANCES


この pin ファクトリがインスタンス化、ピンの現在の数だけでなくピン フィルターごとこの pin ファクトリがインスタンスの最大数。

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

このプロパティは、型 KSPIN の構造体を返す\_CINSTANCES:

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

次に、KSPIN の各メンバーの説明\_CINSTANCES 構造体。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
フィルター処理、または KSINTANCE でピン留めするファクトリをインスタンス化できる pin の最大数を指定します\_中間状態の最大値がない場合。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
フィルターを pin の pin のファクトリがインスタンス化の現在の数を指定します。

このプロパティは、pin の指定した工場出荷時のフィルターごとの最大値を指定します。 使用して、 [ **KSPROPERTY\_PIN\_GLOBALCINSTANCES** ](ksproperty-pin-globalcinstances.md) pin の指定した工場出荷時の全体的な最大値を指定するプロパティ。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

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

 

 





