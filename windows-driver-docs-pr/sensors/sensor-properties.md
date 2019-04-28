---
title: センサーのプロパティ
description: Sensor and Location プラットフォームは、センサーのプロパティを識別する定数を定義します。 センサー メーカーでは、独自のプロパティも定義できます。
ms.assetid: a9f88dad-a81d-45dc-b607-e7b4c5036774
topic_type:
- apiref
api_name:
- SENSOR_PROPERTY_ACCURACY
- SENSOR_PROPERTY_CHANGE_SENSITIVITY
- SENSOR_PROPERTY_CONNECTION_TYPE
- SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL
- SENSOR_PROPERTY_DESCRIPTION
- SENSOR_PROPERTY_DEVICE_PATH
- SENSOR_PROPERTY_FRIENDLY_NAME
- SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE
- SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY
- SENSOR_PROPERTY_MANUFACTURER
- SENSOR_PROPERTY_MIN_REPORT_INTERVAL
- SENSOR_PROPERTY_MODEL
- SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID
- SENSOR_PROPERTY_RANGE_MAXIMUM
- SENSOR_PROPERTY_RANGE_MINIMUM
- SENSOR_PROPERTY_RESOLUTION
- SENSOR_PROPERTY_SERIAL_NUMBER
- SENSOR_PROPERTY_STATE
- SENSOR_PROPERTY_TURN_ON_OFF_NMEA
- SENSOR_PROPERTY_TYPE
- WPD_FUNCTIONAL_OBJECT_CATEGORY
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: df27b7653ba805bac4227aaf1ee15d5e16d62776
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368805"
---
# <a name="sensor-properties"></a>センサーのプロパティ


Sensor and Location プラットフォームは、センサーのプロパティを識別する定数を定義します。 センサー メーカーでは、独自のプロパティも定義できます。

プラットフォームは、次を定義します。 **PROPERTYKEY**センサー プロパティの値。 これらのプロパティとは、それ以外の場合に記載されていない場合は読み取り専用です。

各プラットフォームで定義されているセンサー プロパティ**PROPERTYKEY**共通に基づいて**GUID**という名前のセンサー\_プロパティ\_一般的な\_GUID:

{7F8383EC-D3EC-495C-A8CF-B8BBE85C2920}。

**重要な**  プロパティ キーを定義するこのベース値を使用しないでください。

 

クライアント アプリケーションでに設定可能な読み取り/書き込みとして指定されたプロパティの値。 Static として指定されたプロパティの値は、時間の経過と共に変更しないでください。 センサーでは、必要に応じて指定されたプロパティをサポートする必要です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>キー名のプロパティと PID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_ACCURACY_"></span><span id="sensor_property_accuracy_"></span>
<strong>SENSOR_PROPERTY_ACCURACY</strong> (PID = 17)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>読み取り専用です。 <a href="https://go.microsoft.com/fwlink/p/?linkid=134660" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=134660)">IPortableDeviceValues</a>センサー データの型名と関連付けられているその精度を含むオブジェクト。 精度の値は、true 値から可能なバリエーションを表します。 精度の値は、データ フィールドの場合に特に記載を除く、として、同じ単位を使用して表現されます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CHANGE_SENSITIVITY"></span><span id="sensor_property_change_sensitivity"></span>
<strong>SENSOR_PROPERTY_CHANGE_SENSITIVITY</strong> (PID = 14)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>読み取り/書き込みです。 <strong>IPortableDeviceValues</strong>センサーのデータ型の名前とその関連する変更の秘密度値を格納しているオブジェクト。 値を変更すると小文字の区別は、データ フィールドが使用される、SENSOR_EVENT_DATA_UPDATED イベントが発生する前に変更する必要がありますの金額についての要求を提供します。</p>
<p>秘密度値は、それ以外の場合に記載されている場合を除き、データ フィールドと同じ単位を使用して表現されます。</p>
<p>一部のセンサーの感度の変更は、実際の値として解釈されます。 たとえば、SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS 2 の変更の感度値は、プラスまたはマイナス 2 ℃ の感度を表します。</p>
<p>環境光センサー (ALS) などの他のセンサーの感度の変更は、パーセントとして解釈されます。 そのため、LUX の 2% ずつずらして SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX 2 の感度の変更を表します。</p>
<p>特定の秘密度の変更が、同じセンサーを使用する複数のアプリケーションを要求するには、この値を設定することができます。 そのため、センサーは、感度の変更の場合は true。 その内部ロジックに基づいてを決定します。 たとえば、センサーは任意のアプリケーションから要求される最小感度の変更を常に使用する場合があります。</p>
<p>アプリケーションは、VT_ をこのプロパティを設定、デバイス ドライバーはその既定値に SENSOR_PROPERTY_CHANGE_SENSITIVITY をリセットする必要があります。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_CONNECTION_TYPE"></span><span id="sensor_property_connection_type"></span>
<strong>SENSOR_PROPERTY_CONNECTION_TYPE</strong> (PID = 11)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用です。 <a href="https://msdn.microsoft.com/library/windows/desktop/dd318902" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/dd318902)"><strong>SensorConnectionType</strong> </a>を現在の接続の種類を含む値です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL"></span><span id="sensor_property_current_report_interval"></span>
<strong>SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL</strong> (PID = 13)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込みです。 センサー データの現在の経過時間 (ミリ秒単位) の生成を報告します。</p>
<p>いずれかを返すことを通知する値を 0 に設定します。 既定のレポート間隔、または最小のレポート間隔。 1 つのみのクライアントが接続されている場合は、ドライバーは、既定のレポート間隔を返す必要があります。 複数のクライアントが接続されている場合、ドライバーは、これらのクライアントのいずれかによって要求された最短の間隔を返す必要があります。</p>
<p>アプリケーションは、特定のレポート間隔を要求するには、この値を設定できますが、複数のアプリケーションが同じドライバーを使用します。 そのため、ドライバーは、内部ロジックに基づいて、実際のレポート間隔を決定します。 たとえば、ドライバーは呼び出し元で要求されている最短のレポート間隔を常に使用する場合があります。</p>
<p>このプロパティを使用する方法の例は、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/dd319014" data-raw-source="[Using Sensor API Events](https://msdn.microsoft.com/library/windows/desktop/dd319014)">センサー API イベントを使用した</a>します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_DESCRIPTION"></span><span id="sensor_property_description"></span>
<strong>SENSOR_PROPERTY_DESCRIPTION</strong> (PID = 10)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 センサーの説明文字列です。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_DEVICE_PATH"></span><span id="sensor_property_device_path"></span>
<strong>SENSOR_PROPERTY_DEVICE_PATH</strong> (PID = 15)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 センサーが関連付けられているデバイスのインスタンスを一意に識別します。 このプロパティを使用して、デバイスに複数のセンサーが含まれているかどうかを判断することができます。</p>
<p>デバイス ドライバーをドライバーに問い合わせることがなく、プラットフォームがアプリケーションには、この値を提供するために、このプロパティをサポートする必要はありません。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_FRIENDLY_NAME"></span><span id="sensor_property_friendly_name"></span>
<strong>SENSOR_PROPERTY_FRIENDLY_NAME</strong> (PID = 9)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 デバイスのフレンドリ名。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE"></span><span id="sensor_property_light_response_curve"></span>
<strong>SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>読み取り専用です。 アンビエント ライト レベルとオフセットの間のマッピングを指定する値のペアを含む counted 配列。 これらの値はパーセンテージとして表されます。 適応型輝度調整機能は、Windows では、ユーザーの現在のディスプレイの明るさ設定にこれらの値が適用されます。</p>
<p>ベクター型のデータは常としてシリアル化された<strong>VT_UI1</strong> (符号なし、1 バイト文字の配列)。 このプロパティに実際には 4 バイト符号なし整数としての各値が含まれています (<strong>VT_UI4)</strong>します。 配列の操作については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/desktop/ee264327" data-raw-source="[Retrieving Vector Types](https://msdn.microsoft.com/library/windows/desktop/ee264327)">ベクター型を取得する</a>します。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY"></span><span id="sensor_property_location_desired_accuracy"></span>
<strong>SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY</strong> (PID = 19)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込みです。 値、 <a href="https://msdn.microsoft.com/library/windows/desktop/dd756639" data-raw-source="[&lt;strong&gt;LOCATION_DESIRED_ACCURACY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/dd756639)"> <strong>LOCATION_DESIRED_ACCURACY</strong> </a>クライアント アプリケーションによって要求された精度の処理の種類を示す列挙体。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_DEFAULT</strong> (0)、センサーが対象の電力使用とその他のコストに関する考慮事項を最適化できますが、精度を使用することを示します。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_HIGH</strong> (1)、センサーが、最も正確なレポートを配信することを示します。 これには、可能性があります、料金が請求されるサービスの使用またはより高いレベルのバッテリ電力または接続の帯域幅の消費が含まれます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MANUFACTURER"></span><span id="sensor_property_manufacturer"></span>
<strong>SENSOR_PROPERTY_MANUFACTURER</strong> (PID = 6)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 製造元の名前。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_MIN_REPORT_INTERVAL"></span><span id="sensor_property_min_report_interval"></span>
<strong>SENSOR_PROPERTY_MIN_REPORT_INTERVAL</strong> (PID = 12)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 ミリ秒単位で、センサー データのレポート生成用ハードウェアをサポートする最小間隔。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MODEL"></span><span id="sensor_property_model"></span>
<strong>SENSOR_PROPERTY_MODEL</strong> (PID = 7)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 センサーのモデル名。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID"></span><span id="sensor_property_persistent_unique_id"></span>
<strong>SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID</strong> (PID = 5)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 A <strong>GUID</strong>センサーを識別します。 この値は、デバイス、またはコンピューターの列挙型と同じモデルのデバイス間では、各センサーに対して一意である必要があります。 このプロパティは、呼び出すことによって取得同じ値を含む<a href="https://msdn.microsoft.com/library/windows/desktop/dd318873" data-raw-source="[&lt;strong&gt;ISensor::GetID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/dd318873)"> <strong>ISensor::GetID</strong> </a>します。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RANGE_MAXIMUM"></span><span id="sensor_property_range_maximum"></span>
<strong>SENSOR_PROPERTY_RANGE_MAXIMUM</strong> (PID = 21)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用です。 <strong>IPortableDeviceValues</strong>センサー データ フィールドの名前とその関連付けられている最大値を格納しているオブジェクト。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_RANGE_MINIMUM"></span><span id="sensor_property_range_minimum"></span>
<strong>SENSOR_PROPERTY_RANGE_MINIMUM</strong> (PID = 20)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用です。 <strong>IPortableDeviceValues</strong>センサー データ フィールドの名前とその関連の最小値を格納しているオブジェクト。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RESOLUTION"></span><span id="sensor_property_resolution"></span>
<strong>SENSOR_PROPERTY_RESOLUTION</strong> (PID = 18)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用です。 <strong>IPortableDeviceValues</strong>センサー データ フィールドの名前とその関連する解決策を含むオブジェクト。 解像度の値は、データ フィールドを変更すると小文字の区別を表します。</p>
<p>解像度の値は、それ以外の場合に記載されている場合を除き、データ フィールドと同じ単位を使用して表現されます。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_SERIAL_NUMBER"></span><span id="sensor_property_serial_number"></span>
<strong>SENSOR_PROPERTY_SERIAL_NUMBER</strong> (PID = 8)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 センサーのシリアル番号。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_STATE"></span><span id="sensor_property_state"></span>
<strong>SENSOR_PROPERTY_STATE</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用です。 必須。</p>
<p><a href="https://msdn.microsoft.com/library/windows/desktop/dd318905" data-raw-source="[&lt;strong&gt;SensorState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/dd318905)"><strong>SensorState</strong> </a>センサーの現在の状態を表す値です。</p>
<div class="alert">
<strong>注</strong>このプロパティを更新するを呼び出して、状態変更イベントを発生させる<a href="https://msdn.microsoft.com/library/windows/hardware/ff545523" data-raw-source="[&lt;strong&gt;ISensorClassExtension::PostStateChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545523)"> <strong>ISensorClassExtension::PostStateChange</strong></a>します。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_TURN_ON_OFF_NMEA"></span><span id="sensor_property_turn_on_off_nmea"></span>
<strong>SENSOR_PROPERTY_TURN_ON_OFF_NMEA</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込みです。 TRUE の場合は、データのレポートで、NMEA 文に含まれています。 False の場合、NMEA 文は含まれません。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_TYPE"></span><span id="sensor_property_type"></span>
<strong>SENSOR_PROPERTY_TYPE</strong> (PID = 2)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 A <strong>GUID</strong>センサーの種類を識別します。 プラットフォーム定義されているセンサーの種類は、Sensors.h で定義されます。</p></td>
</tr>
</tbody>
</table>

すべてのセンサーでは、Windows ポータブル デバイス (WPD) の次のプロパティをサポートする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティのキー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="WPD_FUNCTIONAL_OBJECT_CATEGORY"></span><span id="wpd_functional_object_category"></span>
<strong>WPD_FUNCTIONAL_OBJECT_CATEGORY</strong></td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用です。 必要な場合は、静的です。 センサーのカテゴリを定義します。</p></td>
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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**GetProperties**](https://msdn.microsoft.com/library/windows/desktop/dd318874)

[**GetProperty**](https://msdn.microsoft.com/library/windows/desktop/dd318876)

[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=275070)

[**SetProperties**](https://msdn.microsoft.com/library/windows/desktop/dd318899)

 

 






