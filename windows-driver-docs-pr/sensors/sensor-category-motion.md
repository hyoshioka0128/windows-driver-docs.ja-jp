---
title: センサー\_カテゴリ\_モーション
description: センサー\_カテゴリ\_モーションのカテゴリには、物理的な移動に関連する情報を提供するセンサーが含まれています。
ms.assetid: 9189aefc-e92d-483c-80da-f61339b14ebd
keywords:
- SENSOR_CATEGORY_MOTION センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_MOTION
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: cabb7b6cef6f0c1be87675db5aede006f18b213c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551949"
---
# <a name="sensorcategorymotion"></a>センサー\_カテゴリ\_モーション


センサー\_カテゴリ\_モーションのカテゴリには、物理的な移動に関連する情報を提供するセンサーが含まれています。 加速度計センサー、重力加速度などの高速化を測定します。 セキュリティ システム、オブジェクトを移動するという意味で人間の動きの検出などのモーション検出 角度の速度で Gyrometers 意味が変更されます。 円形の速度を測定します。

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
<td><p>SENSOR_TYPE_ACCELEROMETER_1D</p></td>
<td><p>1 つの軸加速度計します。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_ACCELEROMETER_2D</p></td>
<td><p>2 つの軸加速度計します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_ACCELEROMETER_3D</p></td>
<td><p>3 軸加速度計します。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_1D</p></td>
<td><p>1 つの軸 gyrometers します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_GYROMETER_2D</p></td>
<td><p>2 つの軸 gyrometers します。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_3D</p></td>
<td><p>3 軸 gyrometers します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MOTION_DETECTOR</p></td>
<td><p>セキュリティ システムで使用されるものなどのモーション検出</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_SPEEDOMETER</p></td>
<td><p>料金-モーションのセンサー。</p></td>
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
<td><p>SENSOR_DATA_TYPE_ACCELERATION_X_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>X 軸の高速化で、 <em>g</em>秒。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Y_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Y 軸の高速化で、 <em>g</em>秒。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Z_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Z 軸の高速化で、 <em>g</em>秒。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_X_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>1 秒あたりの角度での Gyrometric x 軸加速します。 2 乗。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Y_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric y 軸加速度、1 秒あたりの角度での 2 乗。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Z_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric z 軸加速度、1 秒あたりの角度での 2 乗。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric x 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric y 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric z 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_MOTION_STATE</p></td>
<td><p><strong>VT_BOOL</strong></p></td>
<td><p><strong>VARIANT_TRUE</strong>モーションが検出された場合、それ以外の場合<strong>VARIANT_FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_SPEED_METERS_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>1 秒あたりのメートル単位の速度。</p></td>
</tr>
</tbody>
</table>

 

**重要な**  モーションのプラットフォームで定義されているデータの種類ごと**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_の種類\_モーション\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

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

 

 





