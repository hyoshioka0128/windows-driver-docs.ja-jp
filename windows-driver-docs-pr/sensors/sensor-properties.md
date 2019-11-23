---
title: センサーのプロパティ
description: センサーと場所のプラットフォームでは、センサーのプロパティを識別する定数を定義します。 センサーの製造元は、独自のプロパティを定義することもできます。
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
ms.openlocfilehash: 01b5308caf6b12022a47edadce3fd33101d8c7bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845494"
---
# <a name="sensor-properties"></a>センサーのプロパティ


センサーと場所のプラットフォームでは、センサーのプロパティを識別する定数を定義します。 センサーの製造元は、独自のプロパティを定義することもできます。

プラットフォームでは、センサープロパティの次の**Propertykey**値が定義されています。 特に明記されていない限り、これらのプロパティは読み取り専用です。

各プラットフォーム定義センサープロパティ**Propertykey**は、センサー\_プロパティ\_共通\_guid という名前の共通**GUID**に基づいています。

{7F8383EC-D3EC-495C-A8CF-B8BBE85C2920}.

**重要**   この基本値を使用して、独自のプロパティキーを定義しないでください。

 

読み取り/書き込みとして指定されたプロパティの値は、クライアントアプリケーションで指定できます。 Static として指定されたプロパティの値は、時間の経過と共に変更することはできません。 必須として指定されたプロパティはセンサーによってサポートされる必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティキー名と PID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_ACCURACY_"></span><span id="sensor_property_accuracy_"></span>
<strong>SENSOR_PROPERTY_ACCURACY</strong> (PID = 17)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>読み取り専用。 センサーデータ型名とそれに関連付けられている精度を含む<a href="https://go.microsoft.com/fwlink/p/?linkid=134660" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=134660)">Iportabledevicevalues</a>オブジェクト。 精度の値は、実際の値とは異なる可能性があります。 精度の値は、特に記載がない限り、データフィールドと同じ単位を使用して表されます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CHANGE_SENSITIVITY"></span><span id="sensor_property_change_sensitivity"></span>
<strong>SENSOR_PROPERTY_CHANGE_SENSITIVITY</strong> (PID = 14)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>読み取り/書き込み。 センサーデータ型名とそれに関連付けられている変更感度値を格納する<strong>Iportabledevicevalues</strong>オブジェクト。 秘密度の値を変更すると、SENSOR_EVENT_DATA_UPDATED イベントが発生する前にデータフィールドが変更される量に関する要求が示されます。</p>
<p>機密値は、データフィールドと同じ単位を使用して表されます (特に記載のない場合を除く)。</p>
<p>センサーによっては、変更の感度は実際の値として解釈されます。 たとえば、SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS の変更感度値が2の場合、正または負の2°の感度を表します。</p>
<p>アンビエント光センサー (ALS) のような他のセンサーの場合、変更の感度はパーセントとして解釈されます。 したがって、SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX の2の変更感度は、LUX のプラスまたはマイナス2% を表します。</p>
<p>この値は、特定の変更の感度を要求するように設定できますが、複数のアプリケーションが同じセンサーを使用する可能性があります。 そのため、センサーは、内部ロジックに基づいて、真の変化感度を判断します。 たとえば、センサーは、アプリケーションによって要求された最小の変更感度を常に使用する場合があります。</p>
<p>アプリケーションでこのプロパティを VT_NULL に設定すると、デバイスドライバーは SENSOR_PROPERTY_CHANGE_SENSITIVITY を既定値にリセットする必要があります。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_CONNECTION_TYPE"></span><span id="sensor_property_connection_type"></span>
<strong>SENSOR_PROPERTY_CONNECTION_TYPE</strong> (PID = 11)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用。 現在の接続の種類を含む<a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0002)"><strong>Sensorconnectiontype</strong></a>値。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL"></span><span id="sensor_property_current_report_interval"></span>
<strong>SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL</strong> (PID = 13)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込み。 センサーデータレポート生成の現在の経過時間 (ミリ秒単位)。</p>
<p>値を0に設定すると、ドライバーは、既定のレポート間隔または最小のレポート間隔のどちらかを返すことを通知します。 クライアントが1つしか接続されていない場合、ドライバーは既定のレポート間隔を返します。 複数のクライアントが接続されている場合、ドライバーは、これらのクライアントから要求された最小の間隔を返します。</p>
<p>アプリケーションでは、この値を設定して特定のレポート間隔を要求できますが、複数のアプリケーションが同じドライバーを使用している可能性があります。 そのため、内部ロジックに基づいて、ドライバーは実際のレポート間隔を決定します。 たとえば、ドライバーは常に、任意の呼び出し元によって要求された最短のレポート間隔を使用する場合があります。</p>
<p>このプロパティを使用する方法の例については、「<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/using-sensor-api-events" data-raw-source="[Using Sensor API Events](https://docs.microsoft.com/windows/desktop/SensorsAPI/using-sensor-api-events)">センサー API イベントの使用</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_DESCRIPTION"></span><span id="sensor_property_description"></span>
<strong>SENSOR_PROPERTY_DESCRIPTION</strong> (PID = 10)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 センサーの説明文字列。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_DEVICE_PATH"></span><span id="sensor_property_device_path"></span>
<strong>SENSOR_PROPERTY_DEVICE_PATH</strong> (PID = 15)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 センサーが関連付けられているデバイスインスタンスを一意に識別します。 このプロパティを使用して、デバイスに複数のセンサーが含まれているかどうかを判断できます。</p>
<p>プラットフォームはドライバーにクエリを実行せずにこの値をアプリケーションに提供するため、デバイスドライバーはこのプロパティをサポートする必要はありません。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_FRIENDLY_NAME"></span><span id="sensor_property_friendly_name"></span>
<strong>SENSOR_PROPERTY_FRIENDLY_NAME</strong> (PID = 9)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 Required、static。 デバイスのフレンドリ名。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE"></span><span id="sensor_property_light_response_curve"></span>
<strong>SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>読み取り専用。 アンビエントライトレベルとオフセットの間のマッピングを提供する値のペアを含む、カウントされた配列。 これらの値はパーセンテージで表されます。 Windows の [アダプティブ輝度] 機能では、これらの値がユーザーの現在のディスプレイの明るさの設定に適用されます。</p>
<p>ベクター型のデータは、常に<strong>VT_UI1</strong> (符号なしの1バイト文字の配列) としてシリアル化されます。 このプロパティには、実際には各値が4バイト符号なし整数 (<strong>VT_UI4)</strong>として格納されます。 配列の操作の詳細については、「<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">ベクター型の取得</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY"></span><span id="sensor_property_location_desired_accuracy"></span>
<strong>SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY</strong> (PID = 19)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込み。 クライアントアプリケーションによって要求された精度の処理の種類を示す<a href="https://docs.microsoft.com/previous-versions/windows/desktop/legacy/dd756639(v=vs.85)" data-raw-source="[&lt;strong&gt;LOCATION_DESIRED_ACCURACY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/dd756639(v=vs.85))"><strong>LOCATION_DESIRED_ACCURACY</strong></a>列挙の値。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_DEFAULT</strong> (0) は、センサーが電力使用を最適化するための精度と、その他のコストに関する考慮事項を使用する必要があることを示します。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_HIGH</strong> (1) は、センサーが最も正確なレポートを提供する必要があることを示します。 これには、料金を支払う可能性のあるサービスや、より高いレベルのバッテリ電力または接続帯域幅を消費するサービスの使用が含まれます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MANUFACTURER"></span><span id="sensor_property_manufacturer"></span>
<strong>SENSOR_PROPERTY_MANUFACTURER</strong> (PID = 6)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 Required、static。 製造元の名前。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_MIN_REPORT_INTERVAL"></span><span id="sensor_property_min_report_interval"></span>
<strong>SENSOR_PROPERTY_MIN_REPORT_INTERVAL</strong> (PID = 12)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用。 Required、static。 センサーデータレポートを生成するためにハードウェアがサポートする最小間隔 (ミリ秒単位)。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MODEL"></span><span id="sensor_property_model"></span>
<strong>SENSOR_PROPERTY_MODEL</strong> (PID = 7)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 Required、static。 センサーのモデル名。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID"></span><span id="sensor_property_persistent_unique_id"></span>
<strong>SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID</strong> (PID = 5)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用。 Required、static。 センサーを識別する<strong>GUID</strong> 。 この値は、デバイス上のセンサーごと、またはコンピューターで列挙された同じモデルのデバイス間で一意である必要があります。 このプロパティには、 <a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getid" data-raw-source="[&lt;strong&gt;ISensor::GetID&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getid)"><strong>ISensor:: GetID</strong></a>を呼び出すことによって取得したものと同じ値が格納されます。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RANGE_MAXIMUM"></span><span id="sensor_property_range_maximum"></span>
<strong>SENSOR_PROPERTY_RANGE_MAXIMUM</strong> (PID = 21)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用。 センサーデータフィールド名とそれに関連付けられている最大値を含む<strong>Iportabledevicevalues</strong>オブジェクト。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_RANGE_MINIMUM"></span><span id="sensor_property_range_minimum"></span>
<strong>SENSOR_PROPERTY_RANGE_MINIMUM</strong> (PID = 20)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用。 センサーデータフィールド名とそれに関連付けられている最小値を含む<strong>Iportabledevicevalues</strong>オブジェクト。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RESOLUTION"></span><span id="sensor_property_resolution"></span>
<strong>SENSOR_PROPERTY_RESOLUTION</strong> (PID = 18)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>読み取り専用。 センサーデータフィールド名とそれに関連付けられている解像度を含む<strong>Iportabledevicevalues</strong>オブジェクト。 解決値は、データフィールドの変更に対する感度を表します。</p>
<p>解決値は、特に記載がない限り、データフィールドと同じ単位を使用して表されます。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_SERIAL_NUMBER"></span><span id="sensor_property_serial_number"></span>
<strong>SENSOR_PROPERTY_SERIAL_NUMBER</strong> (PID = 8)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>読み取り専用。 Required、static。 センサーのシリアル番号。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_STATE"></span><span id="sensor_property_state"></span>
<strong>SENSOR_PROPERTY_STATE</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り専用。 必須。</p>
<p>現在のセンサーの状態を含む<a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0001" data-raw-source="[&lt;strong&gt;SensorState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0001)"><strong>Sensorstate</strong></a>値。</p>
<div class="alert">
<strong>メモ</strong> このプロパティを更新するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange" data-raw-source="[&lt;strong&gt;ISensorClassExtension::PostStateChange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)"><strong>ISensorClassExtension::P oststatechange</strong></a>を呼び出して、状態変更イベントを発生させます。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_TURN_ON_OFF_NMEA"></span><span id="sensor_property_turn_on_off_nmea"></span>
<strong>SENSOR_PROPERTY_TURN_ON_OFF_NMEA</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>読み取り/書き込み。 TRUE の場合、NMEA 文はデータレポートに含まれます。 False の場合、NMEA 文は含まれません。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_TYPE"></span><span id="sensor_property_type"></span>
<strong>SENSOR_PROPERTY_TYPE</strong> (PID = 2)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用。 Required、static。 センサーの種類を識別する<strong>GUID</strong> 。 プラットフォームで定義されたセンサーの種類は、センサー .h で定義されています。</p></td>
</tr>
</tbody>
</table>

次の Windows ポータブルデバイス (WPD) プロパティは、すべてのセンサーでサポートされている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティキー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="WPD_FUNCTIONAL_OBJECT_CATEGORY"></span><span id="wpd_functional_object_category"></span>
<strong>WPD_FUNCTIONAL_OBJECT_CATEGORY</strong></td>
<td><p><strong>VT_CLSID</strong></p>
<p>読み取り専用。 Required、static。 センサーカテゴリを定義します。</p></td>
</tr>
</tbody>
</table>

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
<td><p>Header</p></td>
<td>センサー. h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetProperties**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getproperties)

[**GetProperty**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getproperty)

[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=275070)

[**SetProperties**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-setproperties)

 

 






