---
title: センサー\_カテゴリ\_向き
description: センサー\_カテゴリ\_向きのカテゴリには、物理的な方向についての情報を提供するセンサーが含まれています。
ms.assetid: F8089596-C68F-48B2-B4EF-FB7B8777F212
topic_type:
- apiref
api_name:
- SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION
- SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION
- SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION
- SENSOR_TYPE_COMPASS_1D
- SENSOR_TYPE_COMPASS_2D
- SENSOR_TYPE_COMPASS_3D
- SENSOR_TYPE_DISTANCE_1D
- SENSOR_TYPE_DISTANCE_2D
- SENSOR_TYPE_DISTANCE_3D
- SENSOR_TYPE_INCLINOMETER_1D
- SENSOR_TYPE_INCLINOMETER_2D
- SENSOR_TYPE_INCLINOMETER_3D
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_TILT_X_DEGREES
- SENSOR_DATA_TYPE_TILT_Y_DEGREES
- SENSOR_DATA_TYPE_TILT_Z_DEGREES
- SENSOR_DATA_TYPE_DISTANCE_X_METERS
- SENSOR_DATA_TYPE_DISTANCE_Y_METERS
- SENSOR_DATA_TYPE_DISTANCE_Z_METERS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES
- SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES
- SENSOR_DATA_TYPE_ROTATION_MATRIX
- SENSOR_DATA_TYPE_QUATERNION
- SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION
- SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 611fc68432c5e1561d9f2399c43ea0da44ea8868
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569929"
---
# <a name="sensorcategoryorientation"></a>センサー\_カテゴリ\_向き


センサー\_カテゴリ\_向きのカテゴリには、物理的な方向についての情報を提供するセンサーが含まれています。 内臓されているものでは、方位は磁北に基づくものなど、ナビゲーションの方向を指定します。 Inclinometers 傾斜または昇格を測定します。 距離のセンサーでは、センサー、一部のオブジェクトの近接度を測定します。

**プラットフォーム定義されているセンサーの種類**

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
<td><span id="SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION"></span><span id="sensor_type_aggregated_device_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION</strong></td>
<td><p>四元数を返すことによって、場合によっては、回転行列を現在のデバイスの向きを指定します。 (回転行列です省略可能)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION"></span><span id="sensor_type_aggregated_quadrant_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION</strong></td>
<td><p>現在のデバイスの向きを指定します (度単位)。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_type_aggregated_simple_device_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION</strong></td>
<td><p>列挙体として、デバイスの方向を指定します。 (この型が 4 つの一般的な四分区間のいずれかを使用して、デバイスの方向を指定します。0 °、90 度反時計回りに時計回りに、180 カウンター、および 270 度反時計回り。)</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_1D"></span><span id="sensor_type_compass_1d"></span>
<strong>SENSOR_TYPE_COMPASS_1D</strong> {A415F6C5-CB50-49D0-8E62-A8270BD7A26C}</td>
<td><p>1 つの軸内臓されているものです。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_COMPASS_2D"></span><span id="sensor_type_compass_2d"></span>
<strong>SENSOR_TYPE_COMPASS_2D</strong> {15655CC0-997A-4D30-84DB-57CABA3648BB}</td>
<td><p>2 つの軸内臓されているものです。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_3D"></span><span id="sensor_type_compass_3d"></span>
<strong>SENSOR_TYPE_COMPASS_3D</strong> {76B5CE0D-17DD-414D-93A1-E127F40BDF6E}</td>
<td><p>3 軸内臓されているものです。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_1D"></span><span id="sensor_type_distance_1d"></span>
<strong>SENSOR_TYPE_DISTANCE_1D</strong> {5F14AB2F-1407-4306-A93F-B1DBABE4F9C0}</td>
<td><p>センサーの 1 つの軸の距離。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_DISTANCE_2D"></span><span id="sensor_type_distance_2d"></span>
<strong>SENSOR_TYPE_DISTANCE_2D</strong> {5CF9A46C-A9A2-4E55-B6A1-A04AAFA95A92}</td>
<td><p>センサーの 2 つの軸の距離。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_3D"></span><span id="sensor_type_distance_3d"></span>
<strong>SENSOR_TYPE_DISTANCE_3D</strong> {A20CAE31-0E25-4772-9FE5-96608A1354B2}</td>
<td><p>センサーの 3 つの軸の距離。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_1D"></span><span id="sensor_type_inclinometer_1d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_1D</strong> {B96F98C5-7A75-4BA7-94E9-AC868C966DD8}</td>
<td><p>1 つの軸 inclinometers します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_INCLINOMETER_2D"></span><span id="sensor_type_inclinometer_2d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_2D</strong> {AB140F6D-83EB-4264-B70B-B16A5B256A01}</td>
<td><p>2 つの軸 inclinometers します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_3D"></span><span id="sensor_type_inclinometer_3d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_3D</strong> {B84919FB-EA85-4976-8444-6F6F5C6D31DB}</td>
<td><p>3 軸 inclinometers します。</p></td>
</tr>
</tbody>
</table>

**プラットフォーム定義されているデータ フィールド**

このカテゴリのプロパティのプラットフォームで定義されているキーはセンサーに基づく\_データ\_型\_向き\_GUID:

{1637D8A2-4248-4275-865D-558DE84AEDFD}

このカテゴリには、次のプラットフォームで定義されているデータ フィールドが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>データ フィールドの名前と PID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_x_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</strong> (PID = 10)</td>
<td><p><strong>VT_R8</strong></p>
<p>ジャイロ メーター x 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_y_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</strong> (PID = 11)</td>
<td><p><strong>VT_R8</strong></p>
<p>ジャイロ メーター y 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_z_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>ジャイロ メーター z 軸速度、1 秒あたりの角度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_X_DEGREES"></span><span id="sensor_data_type_tilt_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_X_DEGREES</strong> (PID = 2)</td>
<td><p><strong>VT_R4</strong></p>
<p>傾斜計 x 軸角度 (°)。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_TILT_Y_DEGREES"></span><span id="sensor_data_type_tilt_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Y_DEGREES</strong> (PID = 3)</td>
<td><p><strong>VT_R4</strong></p>
<p>傾斜計 y 軸角度 (°)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_Z_DEGREES"></span><span id="sensor_data_type_tilt_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Z_DEGREES</strong> (PID = 4)</td>
<td><p><strong>VT_R4</strong></p>
<p>傾斜計 z 軸角度 (°)。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_X_METERS"></span><span id="sensor_data_type_distance_x_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_X_METERS</strong> (PID = 8)</td>
<td><p><strong>VT_R4</strong></p>
<p>メートル単位の x 軸の距離です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Y_METERS"></span><span id="sensor_data_type_distance_y_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Y_METERS</strong> (PID = 9)</td>
<td><p><strong>VT_R4</strong></p>
<p>メートル単位の y 軸の距離です。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Z_METERS"></span><span id="sensor_data_type_distance_z_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Z_METERS</strong> (PID = 10)</td>
<td><p><strong>VT_R4</strong></p>
<p>メートル単位の z 軸の距離です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_x_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS</strong> (PID = 19)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力計 x 軸フィールド強度、milligauss で。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_y_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS</strong> (PID = 20)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力計 y 軸フィールド強度、milligauss で。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_z_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS</strong> (PID = 21)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力計 z 軸フィールド強度、milligauss で。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES"></span><span id="sensor_data_type_magnetic_heading_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES</strong> (PID = 5)</td>
<td><p><strong>VT_R4</strong></p>
<p>コンパスの x 軸、(度単位)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES"></span><span id="sensor_data_type_magnetic_heading_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES</strong> (PID = 6)</td>
<td><p><strong>VT_R4</strong></p>
<p>コンパスの y 軸、(度単位)。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES"></span><span id="sensor_data_type_magnetic_heading_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES</strong> (PID = 7)</td>
<td><p><strong>VT_R4</strong></p>
<p>コンパスの z 軸を (度単位)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_magnetic_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES</strong> (PID = 11)</td>
<td><p><strong>VT_R8</strong></p>
<p>方位は磁北相対コンパスを補正 (度単位)。 この補正は、コンパスのデバイスは、PC が配置されているレベルの基盤にフラットなレイアウトがあるかのように表される見出し角度の単位をによりします。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_true_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>真北からコンパスを補正 (度単位)。 この補正は、コンパスのデバイスは、PC が配置されているレベルの基盤にフラットなレイアウトがあるかのように表される見出し角度の単位をによりします。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES__"></span><span id="sensor_data_type_magnetic_heading_magnetic_north_degrees__"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES</strong> (PID = 13)</td>
<td><p><strong>VT_R8</strong></p>
<p>方位は磁北 (度単位) を基準とした uncompensated コンパスします。 基準とする、コンパスのデバイスがインストールされている平面上で測定される、見出しの角度の単位が表されます。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES___"></span><span id="sensor_data_type_magnetic_heading_true_north_degrees___"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES</strong> (PID = 14)</td>
<td><p><strong>VT_R8</strong></p>
<p>角度の真北から uncompensated コンパスします。 基準とする、コンパスのデバイスがインストールされている平面上で測定される、見出しの角度の単位が表されます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES"></span><span id="sensor_data_type_quadrant_angle_degrees"></span>
<strong>SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES</strong> (PID = 15)</td>
<td><p><strong>VT_R8</strong></p>
<p>集計された作業領域の向き、(度単位)。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ROTATION_MATRIX"></span><span id="sensor_data_type_rotation_matrix"></span>
<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>3 x 3 回転行列として 3 D 空間内のデバイスの方向を表す配列のカウント (VT_VECTOR |VT_UI1)。</p>
<p>ベクター型のデータは、VT_UI1 として常にシリアル化 (符号なし、1 バイト文字の配列)。 このデータ フィールドは、単精度浮動小数点数 (VT_R4) として、各値を含める必要があります。</p>
<p>この配列は、行列として表されます。</p>
<img src="images/sensor-data-type-rotation-matrix.png" alt="rotation matrix" />
<p>これらの値は回転行列のデータ フィールドの配列には、次のように並べ替えられます。M11、M12、M13、M21、M22...、M23、M31、M32、M33</p>
<p>インボックス Windows 8 の HID センサー クラス ドライバーのサポートを実装するデバイスでは、このデータ フィールドが省略可能なに注意してください。 だけの場合<strong>SENSOR_DATA_TYPE_QUATERNION</strong>が実装されている<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong>が計算され、データ レポートが送信されるごとに設定されます。 インボックス HID センサー クラス ドライバーを使用していないデバイスを計算し、両方を公開する必要があります<strong>SENSOR_DATA_TYPE_QUATERNION</strong>と<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong>センサー データ フィールド。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUATERNION"></span><span id="sensor_data_type_quaternion"></span>
<strong>SENSOR_DATA_TYPE_QUATERNION</strong> (PID = 17)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>X、y、z、3 D 空間内のデバイスの方向を表す四元数の w 値。 (VT_VECTOR |VT_UI1)。</p>
<p>ベクター型のデータは、VT_UI1 として常にシリアル化 (符号なし、1 バイト文字の配列)。</p>
<p>このデータ フィールドは、単精度浮動小数点数 (VT_R4) として、各値を含める必要があります。</p>
<p>この配列内の値の順序のとおりです: [x、y、z、w]</p>
<p>四元数の W 値は [0, 1] に制限されます [-1, 1] フルの代わりにします。</p>
<p>前方向 (およびその逆は不可) は、すべての回転を記述する必要があります。</p>
<p>注:四元数の出力は、正規化された形式である必要があります。 正規化された形式で表現の四元数は、値は、次を満たします。</p>
<img src="images/sensor-data-type-quaternion-formula.png" alt="quaternion formula" /></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_data_type_simple_device_orientation"></span>
<strong>SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION</strong> (PID = 18)</td>
<td><p><strong>VT_UI4</strong></p>
<p>集計されたデバイスの向き、列挙型として指定します。 (列挙値は、四分区間のいずれかに対応)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY"></span><span id="sensor_data_type_magnetometer_accuracy"></span>
<strong>SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY</strong> (PID = 22)</td>
<td><p><strong>VT_I4</strong></p>
<p>磁力計精度の読み取り、列挙型として指定します。</p></td>
</tr>
</tbody>
</table>

<a name="requirements"></a>必要条件
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
<td><p>Header</p></td>
<td>Sensors.h</td>
</tr>
</tbody>
</table>

 

 





