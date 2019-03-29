---
title: センサー\_カテゴリ\_場所
description: センサー\_カテゴリ\_場所のカテゴリには、地理的位置情報を提供するセンサーが含まれています。
ms.assetid: 19B76F17-0575-42F2-ADEF-15932DCE7E06
topic_type:
- apiref
api_name:
- SENSOR_TYPE_LOCATION_BROADCAST
- SENSOR_TYPE_LOCATION_DEAD_RECKONING
- SENSOR_TYPE_LOCATION_GPS
- SENSOR_TYPE_LOCATION_LOOKUP
- SENSOR_TYPE_LOCATION_OTHER
- SENSOR_TYPE_LOCATION_STATIC
- SENSOR_TYPE_LOCATION_TRIANGULATION
- SENSOR_DATA_TYPE_ADDRESS1
- SENSOR_DATA_TYPE_ADDRESS2
- SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS
- SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS
- SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS
- SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS
- SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS
- SENSOR_DATA_TYPE_CITY
- SENSOR_DATA_TYPE_COUNTRY_REGION
- SENSOR_DATA_TYPE_DGPS_DATA_AGE
- SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID
- SENSOR_DATA_TYPE_ERROR_RADIUS_METERS
- SENSOR_DATA_TYPE_FIX_QUALITY
- SENSOR_DATA_TYPE_FIX_TYPE
- SENSOR_DATA_TYPE_GEOIDAL_SEPARATION
- SENSOR_DATA_TYPE_GPS_OPERATION_MODE
- SENSOR_DATA_TYPE_GPS_SELECTION_MODE
- SENSOR_DATA_TYPE_GPS_STATUS
- SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION
- SENSOR_DATA_TYPE_LATITUDE_DEGREES
- SENSOR_DATA_TYPE_LONGITUDE_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_VARIATION
- SENSOR_DATA_TYPE_NMEA_SENTENCE
- SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION
- SENSOR_DATA_TYPE_POSTALCODE
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS
- SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO
- SENSOR_DATA_TYPE_SATELLITES_USED_COUNT
- SENSOR_DATA_TYPE_SATELLITES_USED_PRNS
- SENSOR_DATA_TYPE_SPEED_KNOTS
- SENSOR_DATA_TYPE_STATE_PROVINCE
- SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES
- SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION
api_type:
- NA
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2452edd6c8cfb7bc8df788bc7083c7538e2c09f0
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349471"
---
# <a name="sensorcategorylocation"></a>センサー\_カテゴリ\_場所


センサー\_カテゴリ\_場所のカテゴリには、地理的位置情報を提供するセンサーが含まれています。

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
<td><span id="SENSOR_TYPE_LOCATION_BROADCAST"></span><span id="sensor_type_location_broadcast"></span>
<strong>SENSOR_TYPE_LOCATION_BROADCAST</strong> {D26988CF-5162-4039-BB17-4C58B698E44A}</td>
<td><p>テレビまたは無線周波数などの転送を使用して位置情報を送信するセンサー。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_DEAD_RECKONING"></span><span id="sensor_type_location_dead_reckoning"></span>
<strong>SENSOR_TYPE_LOCATION_DEAD_RECKONING</strong> {1A37D538-F28B-42DA-9FCE-A9D0A2A6D829}</td>
<td><p>配信不能推測センサー。 これらのセンサーでは、まず現在の場所を計算し、モーション データを使用して、現在の場所を更新します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_GPS"></span><span id="sensor_type_location_gps"></span>
<strong>SENSOR_TYPE_LOCATION_GPS</strong> {ED4CA589-327A-4FF9-A560-91DA4B48275E}</td>
<td><p>グローバル配置 system のセンサー。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_LOOKUP"></span><span id="sensor_type_location_lookup"></span>
<strong>SENSOR_TYPE_LOCATION_LOOKUP</strong> {3B2EAE4A-72CE-436D-96D2-3C5B8570E987}</td>
<td><p>ユーザーの IP アドレスに基づいて情報を提供するようなルックアップ センサー。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_OTHER"></span><span id="sensor_type_location_other"></span>
<strong>SENSOR_TYPE_LOCATION_OTHER</strong> {9B2D0566-0368-4F71-B88D-533F132031DE}</td>
<td><p>その他の場所のセンサー。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_STATIC"></span><span id="sensor_type_location_static"></span>
<strong>SENSOR_TYPE_LOCATION_STATIC</strong> {095F8184-0FA9-4445-8E6E-B70F320B6B4C}</td>
<td><p>事前設定された、ユーザー指定の情報を使用するような場所が固定センサー。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_TRIANGULATION"></span><span id="sensor_type_location_triangulation"></span>
<strong>SENSOR_TYPE_LOCATION_TRIANGULATION</strong> {691C341A-5406-4FE1-942F-2246CBEB39E0}</td>
<td><p>携帯電話 tower proximities に基づいて現在の場所を特定するような三角測量センサー。</p></td>
</tr>
</tbody>
</table>

**プラットフォーム定義されているデータ フィールド**

このカテゴリのプロパティのプラットフォームで定義されているキーはセンサーに基づく\_データ\_型\_場所\_GUID:

{055C74D8-CA6F-47D6-95C6-1ED3637A0FF4}

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
<td><span id="SENSOR_DATA_TYPE_ADDRESS1"></span><span id="sensor_data_type_address1"></span>
<strong>SENSOR_DATA_TYPE_ADDRESS1</strong> (PID = 23)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>番地、最初の行。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ADDRESS2"></span><span id="sensor_data_type_address2"></span>
<strong>SENSOR_DATA_TYPE_ADDRESS2</strong> (PID = 24)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>番地、2 番目の行。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_antenna_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS</strong> (PID = 36)</td>
<td><p><strong>VT_R8</strong></p>
<p>メートル単位の sea のレベルに参照されているアンテナの高度です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS</strong> (PID = 29)</td>
<td><p><strong>VT_R8</strong></p>
<p>高度を参照して、メートル単位で、世界測地システム (WGS 84) の参照の楕円体にエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS</strong> (PID = 5)</td>
<td><p><strong>VT_R8</strong></p>
<p>高度のメートル単位で、世界測地システム (WGS 84) の参照の楕円体に参照されています。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS"></span><span id="sensor_data_type_altitude_sealevel_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS</strong> (PID = 30)</td>
<td><p><strong>VT_R8</strong></p>
<p>高度のメートル単位の sea のレベルに参照されているとしてエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS</strong> (PID = 4)</td>
<td><p><strong>VT_R8</strong></p>
<p>メートル単位の sea のレベルに参照されている高度です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_CITY"></span><span id="sensor_data_type_city"></span>
<strong>SENSOR_DATA_TYPE_CITY</strong> (PID = 25)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>市区町村。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_COUNTRY_REGION"></span><span id="sensor_data_type_country_region"></span>
<strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong> (PID = 28)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>国または地域、ISO 3166 1-alpha 2 国/地域コードとして表されます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DGPS_DATA_AGE"></span><span id="sensor_data_type_dgps_data_age"></span>
<strong>SENSOR_DATA_TYPE_DGPS_DATA_AGE</strong> (PID = 35)</td>
<td><p><strong>VT_R8</strong></p>
<p>秒単位で、差分の GPS データの期間。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID"></span><span id="sensor_data_type_differential_reference_station_id"></span>
<strong>SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID</strong> (PID = 37)</td>
<td><p><strong>VT_I4</strong></p>
<p>差分の参照をステーションの ID。 範囲は、0000 ~ 1023 です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ERROR_RADIUS_METERS"></span><span id="sensor_data_type_error_radius_meters"></span>
<strong>SENSOR_DATA_TYPE_ERROR_RADIUS_METERS</strong> (PID = 22)</td>
<td><p><strong>VT_R8</strong></p>
<p>緯度と経度の値をメートル単位の精度。 値 0 は、精度のレベルが不明を意味します。 Location API では、このフィールドに 0 以外の値を提供するセンサーを優先します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_FIX_QUALITY"></span><span id="sensor_data_type_fix_quality"></span>
<strong>SENSOR_DATA_TYPE_FIX_QUALITY</strong> (PID = 10)</td>
<td><p><strong>VT_I4</strong></p>
<p>品質を修正します。</p>
<p>0 = 修正プログラムはありません</p>
<p>1 = GPS</p>
<p>2 = DGPS</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_FIX_TYPE"></span><span id="sensor_data_type_fix_type"></span>
<strong>SENSOR_DATA_TYPE_FIX_TYPE</strong> (PID = 11)</td>
<td><p><strong>VT_I4</strong></p>
<p>種類を修正します。</p>
<p>0 = 修正プログラムはありません</p>
<p>1 = GPS SP モードでは、有効な修正プログラム</p>
<p>2 = DGPS SP モードでは、有効な修正プログラム</p>
<p>3 = GPS PPS モードでは、有効な修正プログラム</p>
<p>4 = リアルタイム運動</p>
<p>5 = float RTK</p>
<p>6 = (盛期配信不能) の推定</p>
<p>7 = 手動入力モード</p>
<p>8 = simulator モード</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GEOIDAL_SEPARATION"></span><span id="sensor_data_type_geoidal_separation"></span>
<strong>SENSOR_DATA_TYPE_GEOIDAL_SEPARATION</strong> (PID = 34)</td>
<td><p><strong>VT_R8</strong></p>
<p>WGS 84 の楕円体と平均の差 sea レベル。 0 より小さい値を示すその平均海面下の参照の楕円体です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_OPERATION_MODE"></span><span id="sensor_data_type_gps_operation_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_OPERATION_MODE</strong> (PID = 32)</td>
<td><p><strong>VT_I4</strong></p>
<p>操作モード。</p>
<p>0 = 手動です。 GPS センサーは、2 D または 3-D モードで動作に設定されます。</p>
<p>1 = 自動。 GPS センサーは、自動的に、2-d および 3-D モードは切り替えることができます。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GPS_SELECTION_MODE"></span><span id="sensor_data_type_gps_selection_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_SELECTION_MODE</strong> (PID = 31)</td>
<td><p><strong>VT_I4</strong></p>
<p>選択モード。</p>
<p>0 = Autonomous します。</p>
<p>1 = DGPS します。</p>
<p>2 = (盛期配信不能) を推定します。</p>
<p>3 = 手動で入力します。</p>
<p>4 = シミュレーター。</p>
<p>5 = データが無効です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_STATUS"></span><span id="sensor_data_type_gps_status"></span>
<strong>SENSOR_DATA_TYPE_GPS_STATUS</strong> (PID = 33)</td>
<td><p><strong>VT_I4</strong></p>
<p>現在のデータの状態です。</p>
<p>1 = データが無効です。</p>
<p>2 = データが無効です。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_horizonal_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION</strong> (PID = 13)</td>
<td><p><strong>VT_R8</strong></p>
<p>有効桁数の種の水平方向。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_LATITUDE_DEGREES"></span><span id="sensor_data_type_latitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LATITUDE_DEGREES</strong> (PID = 2)</td>
<td><p><strong>VT_R8</strong></p>
<p>度の緯度。 North が正の値です。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_LONGITUDE_DEGREES"></span><span id="sensor_data_type_longitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LONGITUDE_DEGREES</strong> (PID = 3)</td>
<td><p><strong>VT_R8</strong></p>
<p>経度の度です。 東部が正の値です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES"></span><span id="sensor_data_type_magnetic_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES</strong> (PID = 8)</td>
<td><p><strong>VT_R8</strong></p>
<p>見出し、(度単位) は磁北に関連します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_VARIATION"></span><span id="sensor_data_type_magnetic_variation"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_VARIATION</strong> (PID = 9)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁流のバリエーション。 東部が正の値です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_NMEA_SENTENCE"></span><span id="sensor_data_type_nmea_sentence"></span>
<strong>SENSOR_DATA_TYPE_NMEA_SENTENCE</strong> (PID = 38)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>現在の NMEA 文文字列です。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_position_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>有効桁数の種の位置。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_POSTALCODE"></span><span id="sensor_data_type_postalcode"></span>
<strong>SENSOR_DATA_TYPE_POSTALCODE</strong> (PID = 27)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>郵便番号。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW"></span><span id="sensor_data_type_satellites_in_view"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW</strong> (PID = 17)</td>
<td><p><strong>VT_I4</strong></p>
<p>ビューでサテライトの数。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH"></span><span id="sensor_data_type_satellites_in_view_azimuth"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH</strong> (PID = 20)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>ビュー内の各サテライト方位角を含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドに実際には、IEEE 8 バイト実際の値としては、各値が含まれています (<strong>vt _ を付けます R8</strong>)。 空の値のプレース ホルダーとして-1 を使用します。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION"></span><span id="sensor_data_type_satellites_in_view_elevation"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION</strong> (PID = 19)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>ビュー内の各サテライトの昇格を含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドに実際には、IEEE 8 バイト実際の値としては、各値が含まれています (<strong>VT_R8</strong>)。 空の値のプレース ホルダーとして-91 を使用します。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID"></span><span id="sensor_data_type_satellites_in_view_id"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID</strong> (PID = 39)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>ビュー内の各サテライトの ID を含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドに実際には 4 バイト符号なし整数としての各値が含まれています (<strong>VT_UI4</strong>)。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS"></span><span id="sensor_data_type_satellites_in_view_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS</strong> (PID = 18)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>サテライトの擬似ノイズ コードをビューに格納する配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドに実際には 4 バイト符号なし整数としての各値が含まれています (<strong>VT_UI4</strong>)。 空の値のプレース ホルダーとしてゼロ (0) を使用します。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS"></span><span id="sensor_data_type_satellites_used_prns_and_constellations"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS</strong> (PID = 41)</td>
<td><p><strong>VT_VECTOR|VT_UI2</strong></p>
<p>ソリューションで使用されているサテライトの擬似ノイズ コードを含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI2</strong> (符号なし、2 バイト文字の配列)。 このデータ フィールドは 4 バイト符号なし整数としての各値を含める必要があります (<strong>VT_UI4</strong>)。 空の値のプレース ホルダーとしてゼロ (0) を使用します。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO"></span><span id="sensor_data_type_satellites_in_view_stn_ratio"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO</strong> (PID = 21)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>ビューで衛星の信号雑音比率を含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドに実際には、IEEE 8 バイト実際の値としては、各値が含まれています (<strong>VT_R8</strong>)。 空の値のプレース ホルダーとしてゼロ (0) を使用します。</p>
<p>このプロパティは、必要なすべての GPS デバイスでサポートする必要があります。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_COUNT"></span><span id="sensor_data_type_satellites_used_count"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_COUNT</strong> (PID = 15)</td>
<td><p><strong>VT_I4</strong></p>
<p>ソリューションで使用されているサテライトの数。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS"></span><span id="sensor_data_type_satellites_used_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>ソリューションで使用されているサテライトの擬似ノイズ コードを含む配列をカウントします。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このデータ フィールドは 4 バイト符号なし整数としての各値を含める必要があります (<strong>VT_UI4</strong>)。 空の値のプレース ホルダーとしてゼロ (0) を使用します。</p>
<p>配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SPEED_KNOTS"></span><span id="sensor_data_type_speed_knots"></span>
<strong>SENSOR_DATA_TYPE_SPEED_KNOTS</strong> (PID = 6)</td>
<td><p><strong>VT_R8</strong></p>
<p>速度、ノットです。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_STATE_PROVINCE"></span><span id="sensor_data_type_state_province"></span>
<strong>SENSOR_DATA_TYPE_STATE_PROVINCE</strong> (PID = 26)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>都道府県。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES"></span><span id="sensor_data_type_true_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES</strong> (PID = 7)</td>
<td><p><strong>VT_R8</strong></p>
<p>関連度では、真北見出しです。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_vertical_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION</strong> (PID = 14)</td>
<td><p><strong>VT_R8</strong></p>
<p>有効桁数の種の垂直方向。</p></td>
</tr>
</tbody>
</table>

 

 





