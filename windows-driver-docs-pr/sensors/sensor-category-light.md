---
title: センサー\_カテゴリ\_ライト
description: センサー\_カテゴリ\_ライトのカテゴリには、光の特性に関する情報を提供するセンサーが含まれています。
ms.assetid: 56bb4869-3752-437d-89c9-829e6fb01043
keywords:
- SENSOR_CATEGORY_LIGHT センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_LIGHT
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4ca05c45f2f7c03d93c450bc41a6febf266d8ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538175"
---
# <a name="sensorcategorylight"></a>センサー\_カテゴリ\_ライト


センサー\_カテゴリ\_ライトのカテゴリには、光の特性に関する情報を提供するセンサーが含まれています。

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
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_TYPE_AMBIENT_LIGHT</p></td>
<td><p>環境光センサーです。</p></td>
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
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_LIGHT_CHROMACITY</p></td>
<td><p><strong>VT_VECTOR</strong>|<strong>VT_UI1</strong></p></td>
<td><p>浮動小数値のカウントの配列としてが一番です。</p>
<p>ベクター型のデータは、VT_UI1 として常にシリアル化 (符号なし、1 バイト文字の配列)。 このデータ フィールドは、IEEE (VT_R4) 4 バイト実際値として、各値を含める必要があります。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX</p></td>
<td><p><strong>VT_R4</strong></p></td>
<td><p>Lux でルクス レベル。</p>
<p></p>
<p>デバイス ドライバーは、また VT_UI4 の型の場合は、このデータ フィールドを処理する必要がありますに注意してください。 (この要件は、Windows 8 より前に製造光センサーの存在します)。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_LIGHT_TEMPERATURE_KELVIN</p></td>
<td><p><strong>VT_R4</strong></p></td>
<td><p>色温度、ケルビンでします。</p></td>
</tr>
</tbody>
</table>

 

**重要な**  プラットフォーム定義されている軽量のデータの種類ごと**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_の種類\_LIGHT\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

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

 

 





