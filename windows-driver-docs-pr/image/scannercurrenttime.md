---
title: ScannerCurrentTime 要素
description: 必要な ScannerCurrentTime 要素は、現在の日付と時刻に従って、スキャナーの内部時計を示します。
ms.assetid: 7103fdb4-dfa4-40b0-b20e-022e2a42bf5c
keywords:
- ScannerCurrentTime 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerCurrentTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ca5252e639acd9ae6d72c82ed55e1986849c6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580040"
---
# <a name="scannercurrenttime-element"></a>ScannerCurrentTime 要素


必要な**ScannerCurrentTime**要素は、現在の日付と時刻に従って、スキャナーの内部時計を示します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerCurrentTime>
  text
</wscn:ScannerCurrentTime>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 DateTime 型の任意の有効な値。 DateTime の詳細については、XML Schema Part 2 を参照してください。Datatypes Second Edition。**dateTimedateTime**

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

スキャナーの内部時計はリアルタイム クロックではありません。 クロックは、0 から開始できます (0001-01-01T00:00:00Z) までカウントするデバイスをオンにすると開始します。

すべての時刻が起動時に、時間に基づいているため、クライアントが読み取ることによって期間と相対的な時間を計算できます、 **ScannerCurrentTime**要素と前の時刻の値と比較します。

## <a name="see-also"></a>関連項目


[**ScannerStatus**](scannerstatus.md)

 

 






