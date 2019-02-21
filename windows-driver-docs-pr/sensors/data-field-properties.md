---
title: データ フィールドのプロパティ
description: このトピックでは、データ フィールドでのみ使用されるセンサー プロパティについて説明します。
ms.assetid: A7FA02AA-7B7B-45B4-A432-4B4ED69CB19C
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9797282dafe6f2db5b2a8408b963d783781ac16c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559088"
---
# <a name="data-field-properties"></a>データ フィールドのプロパティ


このトピックでは、データ フィールドでのみ使用されるセンサー プロパティについて説明します。

次の表では、センサーのプロパティを示します。 これらのプロパティは、任意のデータ フィールドに適用ので、型によって異なりますデータ フィールドこれらのプロパティが参照するを参照してください、[センサー データ フィールド](sensor-data-fields.md)についても説明します。

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
<th>プロパティのキー</th>
<th>種類</th>
<th>アクセス (R/O、読み取り/書き込み)</th>
<th>必須/オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorDataField_Resolution</p></td>
<td><p>入力データ フィールドを参照してください。</p></td>
<td><p>R/O</p></td>
<td><p>これは、データ フィールドに依存し、プロパティの一覧についてはこのデータ フィールドを必要とするキーを参照してください、<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">データ フィールドのプロパティに必要な</a>トピック。</p></td>
<td><p>データ フィールドの解像度。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorDataField_RangeMinimum</p></td>
<td><p>入力データ フィールドを参照してください。</p></td>
<td><p>R/O</p></td>
<td><p>これは、データ フィールドに依存し、プロパティの一覧についてはこのデータ フィールドを必要とするキーを参照してください、<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">データ フィールドのプロパティに必要な</a>トピック。</p></td>
<td><p>データ フィールドの最小値。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorDataField_RangeMaximum</p></td>
<td><p>入力データ フィールドを参照してください。</p></td>
<td><p>R/O</p></td>
<td><p>これは、データ フィールドに依存し、プロパティの一覧についてはこのデータ フィールドを必要とするキーを参照してください、<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">データ フィールドのプロパティに必要な</a>トピック。</p></td>
<td><p>データ フィールドの最大値。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** Sensorsdef.h

## <a name="related-topics"></a>関連トピック


[必要なデータ フィールドのプロパティ](required-data-field-properties.md)

[センサー データ フィールド](sensor-data-fields.md)

[センサーのプロパティ](sensor-properties2.md)

 

 






