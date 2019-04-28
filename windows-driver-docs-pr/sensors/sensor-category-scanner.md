---
title: センサー\_カテゴリ\_スキャナー
description: センサー\_カテゴリ\_スキャナーのカテゴリには、スキャンすることによって取得された情報を提供するセンサーが含まれています。
ms.assetid: ba7a44d0-1d89-4a6c-b046-c7cd02c457b3
keywords:
- SENSOR_CATEGORY_SCANNER センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_SCANNER
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb25e6437e2c5408b77880a108d13f29699cb48c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370429"
---
# <a name="sensorcategoryscanner"></a>センサー\_カテゴリ\_スキャナー


センサー\_カテゴリ\_スキャナーのカテゴリには、スキャンすることによって取得された情報を提供するセンサーが含まれています。

### <a name="span-idplatformdefinedsensortypesspanspan-idplatformdefinedsensortypesspanplatform-defined-sensor-types"></a><span id="platform_defined_sensor_types"></span><span id="PLATFORM_DEFINED_SENSOR_TYPES"></span>プラットフォーム定義されているセンサーの種類

このカテゴリには、次のプラットフォームで定義されているセンサーの種類が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>センサーの種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_TYPE_BARCODE_SCANNER</p></td>
<td><p>光学スキャンを使用してバーコードを読み取るセンサー。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_RFID_SCANNER</p></td>
<td><p>無線周波数の ID がセンサーをスキャンします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idplatformdefineddatafieldsspanspan-idplatformdefineddatafieldsspanplatform-defined-data-fields"></a><span id="platform_defined_data_fields"></span><span id="PLATFORM_DEFINED_DATA_FIELDS"></span>プラットフォーム定義されているデータ フィールド

このカテゴリには、次のプラットフォームで定義されているデータ フィールドが含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>データの種類</th>
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_RFID_TAG_40_BIT</p></td>
<td><p><strong>VT_UI8</strong></p></td>
<td><p>40 ビットの無線周波数 ID タグの値です。</p></td>
</tr>
</tbody>
</table>

 

**重要な**  スキャナーのプラットフォームで定義されているデータの種類ごと**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_型\_スキャナー\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 7</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 7 で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Sensors.h</td>
</tr>
</tbody>
</table>

 

 





