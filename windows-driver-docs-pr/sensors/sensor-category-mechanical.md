---
title: センサー\_カテゴリ\_機械的な
description: センサー\_カテゴリ\_メカニズムに関連する情報を提供するセンサーが機械的なカテゴリに含まれています。
ms.assetid: 0ae66a5b-6564-4e2c-a6a1-c88c7e853a38
keywords:
- SENSOR_CATEGORY_MECHANICAL センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_MECHANICAL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c8b3ae3814050d922287f8c1fd6831e50afa87e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370434"
---
# <a name="sensorcategorymechanical"></a>センサー\_カテゴリ\_機械的な


センサー\_カテゴリ\_メカニズムに関連する情報を提供するセンサーが機械的なカテゴリに含まれています。

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
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH</p></td>
<td><p>2 つの状態スイッチ (無効または上)。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_FORCE</p></td>
<td><p>センサーを強制します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH</p></td>
<td><p>複数の位置に切り替えます。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_PRESSURE</p></td>
<td><p>圧力センサー。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_SCALE</p></td>
<td><p>重量センサー。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_STRAIN</p></td>
<td><p>歪みセンサー。</p></td>
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
<td><p>SENSOR_DATA_TYPE_ABSOLUTE_PRESSURE_PASCAL</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>パスカルでの絶対不足します。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_BOOLEAN_SWITCH_STATE</p></td>
<td><p><strong>VT_BOOL</strong></p></td>
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH 状態フィールドです。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_FORCE_NEWTONS</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>ニュートンの力です。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_GAUGE_PRESSURE_PASCAL</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>相対パスでは、パスカルでの負荷を測定します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_MULTIVALUE_SWITCH_STATE</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH 状態フィールドです。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_STRAIN</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>歪みします。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_WEIGHT_KILOGRAMS</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>キログラムでの重み。</p></td>
</tr>
</tbody>
</table>

 

**重要な**  機械的なデータのプラットフォームで定義されている各種**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_型\_機械的な\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

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

 

 





