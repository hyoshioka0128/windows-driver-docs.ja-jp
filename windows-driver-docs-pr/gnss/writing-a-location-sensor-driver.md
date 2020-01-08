---
title: Windows 8.1 用位置センサー ドライバーの作成
description: Windows 8.1 用位置センサー ドライバーの作成
ms.assetid: 18852282-6529-4934-a448-b699e01987de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0d90d2facc45448a788626675869304b062ade
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652962"
---
# <a name="writing-a-location-sensor-driver-for-windows-81"></a>Windows 8.1 用位置センサー ドライバーの作成

ここでは、場所データを提供するデバイス用のドライバーの作成に関する具体的なガイダンスを提供します。 このセクションに記載されている情報に加えて、場所ドライバーの作成者は、「[センサーデバイスドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/sensors/writing-a-sensor-device-driver)」に記載されている情報を理解し、適用する必要があります。

センサーと場所のプラットフォームには、ソフトウェア開発者がプログラムに場所の機能を簡単に追加できるようにするための Windows Location API が用意されています。 場所センサー用のドライバーを作成する場合は、ドライバーを Location API と互換性があるかどうかを理解し、「場所ドライバーのガイドライン」のガイドラインに従って[電源とパフォーマンスを](location-driver-guidelines-for-power-and-performance.md)確保する必要があります。

## <a name="windows-hardware-certification-program-requirements"></a>Windows ハードウェア認定プログラムの要件

Windows ハードウェア認定プログラムを使用すると、ハードウェアの製造元は、デバイスが Windows を操作するために必要な標準を満たしていることを証明する認定を受けることができます。 認定プログラムでは、センサーの場所やセンサーの種類の要件について説明します。 場所センサードライバーをすべての認定プログラムの要件に準拠させる必要があります。 次の要件があります。

-   場所センサーは、必要なデータとセンサーのプロパティのセットをサポートしている必要があります。

-   場所センサーでは、少なくとも1つの組み込みデータレポートの種類に必要なデータフィールドがサポートされている必要があります。

一般に、この WDK ドキュメントに記載されている推奨事項は、認定プログラムの要件と一致します。 ただし、承認のために送信するセンサードライバーを作成する場合は、公式の認定プログラムに関するドキュメントを確認する必要があります。 Windows ハードウェア認定プログラムの詳細については、 [Windows Hardware Developer Central](https://developer.microsoft.com/windows/hardware)の web サイトを参照してください。

## <a name="location-api-requirements"></a>Location API の要件

センサーの他のカテゴリと同じドライバーモデルとクラス拡張を使用して、場所センサー用のドライバーを作成します。 場所センサーとして機能するためには、少なくとも次のものが必要です。

-   Location カテゴリに属する場所センサーを特定します。

-   センサーの種類を、いずれかの場所センサーの種類に設定します。

-   センサーが提供する場所レポートデータフィールドを特定します。

-   必須プロパティをサポートします。

-   要求されたときにデータを提供します。

-   状態遷移を管理します。

-   データ更新イベントと状態変更イベントを発生させます。

このセクションの残りの部分では、これらの最小要件について説明します。

## <a name="identifying-the-category"></a>カテゴリを識別する

[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を通じて呼び出された場合は、 **WPD\_機能\_オブジェクトの\_category**プロパティ値を**センサー\_カテゴリ\_場所**に設定します。 次のコード例は、pValues という名前の[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)へのポインターを使用して、この定数を設定する方法を示しています。

```cpp
hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, SENSOR_CATEGORY_LOCATION);
```

## <a name="setting-the-location-sensor-type"></a>場所センサーの種類の設定

[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を通じて呼び出された場合は、**センサー\_プロパティ\_TYPE**プロパティ値を正しい値に設定します。 次のコード例は、センサーを使用してセンサーの種類を設定する方法を示しています。そのためには、**センサー\_type\_LOCATION\_GPS**定数を使用します。 pvalues という名前の[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)へのポインターを使用します。

```cpp
hr = pValues->SetGuidValue(SENSOR_PROPERTY_TYPE, SENSOR_TYPE_LOCATION_GPS);
```

## <a name="identifying-the-supported-data-fields"></a>サポートされるデータフィールドの特定

Location API は、2種類の場所レポートを定義します。 これらは、場所データを編成するオブジェクトです。 LatLong レポートには、緯度、経度、および標高のデータフィールドと、エラー範囲情報を含むデータフィールドが含まれています。 都市の住所レポートには、市区町村や郵便番号などの番地のデータフィールドが含まれています。 この2つのデータレポートの種類の少なくとも1つについて、場所ドライバーが必要なデータフィールドをサポートしている必要があります。

LatLong レポートをサポートするには、次のデータフィールドが必要です。

-   センサー\_データ\_型\_緯度\_度
-   センサー\_データ\_種類\_経度\_度
-   センサー\_データ\_種類\_エラー\_RADIUS\_メーター

都市の住所レポートをサポートするには、次のデータフィールドの少なくとも1つが必要です。

-   センサー\_データ\_種類\_国\_地域

(プラットフォームで定義された場所のデータフィールドの完全なセットを表示するには、「 [Windows センサーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」セクションの「[**センサー\_カテゴリ\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-category-loc)」を参照してください)。

[**ISensorDriver:: OnGetSupportedDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)を通じて呼び出された場合、サポートされるデータフィールドプロパティのキー定数を[Iportabledevicekeycollection](https://go.microsoft.com/fwlink/p/?linkid=131484)に追加します。これは、 *ppsupporteddatafields*パラメーターを通じて返されます。 次のコード例では、pKeyCollection という変数を使用して、郵便番号データフィールドを[Iportabledevicekeycollection](https://go.microsoft.com/fwlink/p/?linkid=131484)に追加する方法を示します。

```cpp
pKeyCollection->Add(SENSOR_DATA_TYPE_POSTALCODE);
```

## <a name="support-the-required-properties"></a>必須プロパティをサポートする

他のセンサードライバーと同様に、場所ドライバーは一連のプロパティを使用してセンサー自体に関する情報を提供します。 Windows ハードウェア認定プログラムでは、場所センサーがサポートする必要があるプロパティの最小セットを指定します。 センサーのプロパティとその意味、およびセンサードライバーに必要なプロパティの詳細については、「[**センサーのプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)」を参照してください。 次の一覧には、必要なプロパティが含まれています。

-   WPD\_機能\_オブジェクト\_カテゴリ

-   センサー\_プロパティ\_型

-   センサー\_プロパティ\_状態

-   センサー\_プロパティ\_永続的\_一意\_ID

-   センサー\_プロパティ\_の製造元

-   センサー\_プロパティ\_モデル

-   センサー\_プロパティ\_シリアル\_番号

-   センサー\_プロパティ\_フレンドリ\_名

-   センサー\_プロパティ\_最小\_レポート\_間隔

-   センサー\_プロパティ\_現在の\_レポート\_間隔

-   センサー\_プロパティ\_の場所\_必要な\_精度を持つ

## <a name="providing-data"></a>データの提供

場所ドライバーは、他のセンサードライバーと同じメカニズムを使用してデータを提供します。 つまり、センサークラス拡張は[**ISensorDriver:: OnGetDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)を使用してドライバーを呼び出し、ドライバーは*ppdatavalues*パラメーターを使用して値を返します。

次の要件は、場所センサーからデータを提供する場合に適用されます。

-   同期要求を使用してデータを提供し、[イベントを発生](https://docs.microsoft.com/windows-hardware/drivers/sensors/raising-events)させます。

-   最新のデータレポートのコピーを保持します。 要求時に新しいデータを使用できない場合は、キャッシュされたレポートを返します。 タイムスタンプは更新しないでください。

-   センサー\_データ\_型\_緯度\_度およびセンサー\_データ\_型\_経度\_度の値を指定して、実際の緯度と経度の範囲を超えないようにします。

-   センサー\_データ\_種類\_エラー\_半径\_0 以下の値を報告しないでください。

-   センサー\_データ\_TYPE\_COUNTRY\_REGION の値を、有効な ISO 3166 1-α2国コードに設定します。

-   ドライバーが緯度/経度と都市の両方の住所レポートをサポートしている場合、これらのレポートの場所データは、同じ物理的な場所に対応している必要があります。

次の表では、Location API データレポートフィールドに対応する[センサーデータフィールド](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-categories--types--and-data-fields)について説明します。 場所のデータレポートを提供するときに、これらのデータフィールド定数を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>センサー定数</th>
<th>Location API メソッドとプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ADDRESS1</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157816" data-raw-source="[ICivicAddressReport::GetAddressLine1](https://go.microsoft.com/fwlink/p/?linkid=157816)">ICivicAddressReport::GetAddressLine1</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157817" data-raw-source="[LocationDisp.DispCivicAddressReport.AddressLine1](https://go.microsoft.com/fwlink/p/?linkid=157817)">LocationDisp.DispCivicAddressReport.AddressLine1</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_ADDRESS2</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157818" data-raw-source="[ICivicAddressReport::GetAddressLine2](https://go.microsoft.com/fwlink/p/?linkid=157818)">ICivicAddressReport::GetAddressLine2</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157820" data-raw-source="[LocationDisp.DispCivicAddressReport.AddressLine2](https://go.microsoft.com/fwlink/p/?linkid=157820)">LocationDisp.DispCivicAddressReport.AddressLine2</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157823" data-raw-source="[ILatLongReport::GetAltitudeError](https://go.microsoft.com/fwlink/p/?linkid=157823)">ILatLongReport::GetAltitudeError</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157824" data-raw-source="[LocationDisp.DispLatLongReport.AltitudeError](https://go.microsoft.com/fwlink/p/?linkid=157824)">LocationDisp.DispLatLongReport.AltitudeError</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157825" data-raw-source="[ILatLongReport::GetAltitude](https://go.microsoft.com/fwlink/p/?linkid=157825)">ILatLongReport::GetAltitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157827" data-raw-source="[LocationDisp.DispLatLongReport.Altitude](https://go.microsoft.com/fwlink/p/?linkid=157827)">LocationDisp.DispLatLongReport.Altitude</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_CITY</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157828" data-raw-source="[ICivicAddressReport::GetCity](https://go.microsoft.com/fwlink/p/?linkid=157828)">ICivicAddressReport::GetCity</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157830" data-raw-source="[LocationDisp.DispCivicAddressReport.City](https://go.microsoft.com/fwlink/p/?linkid=157830)">DispCivicAddressReport. 市区町村</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City" data-raw-source="[Windows.Devices. Geolocation.CivicAddress](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City)">Windows. CivicAddress</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157831" data-raw-source="[ICivicAddressReport::GetCountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157831)">ICivicAddressReport::GetCountryRegion</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157832" data-raw-source="[LocationDisp.DispCivicAddressReport.CountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157832)">LocationDisp</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ERROR_RADIUS_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157834" data-raw-source="[ILatLongReport::GetErrorRadius](https://go.microsoft.com/fwlink/p/?linkid=157834)">ILatLongReport::GetErrorRadius</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157835" data-raw-source="[LocationDisp.DispLatLongReport.ErrorRadius](https://go.microsoft.com/fwlink/p/?linkid=157835)">LocationDisp.DispLatLongReport.ErrorRadius</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_LATITUDE_DEGREES</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157836" data-raw-source="[ILatLongReport::GetLatitude](https://go.microsoft.com/fwlink/p/?linkid=157836)">ILatLongReport::GetLatitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157839" data-raw-source="[LocationDisp.DispLatLongReport.Latitude](https://go.microsoft.com/fwlink/p/?linkid=157839)">LocationDisp.DispLatLongReport.Latitude</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_LONGITUDE_DEGREES</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157840" data-raw-source="[ILatLongReport::GetLongitude](https://go.microsoft.com/fwlink/p/?linkid=157840)">ILatLongReport::GetLongitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157841" data-raw-source="[LocationDisp.DispLatLongReport.Longitude](https://go.microsoft.com/fwlink/p/?linkid=157841)">LocationDisp.DispLatLongReport.Longitude</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_POSTALCODE</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157842" data-raw-source="[ICivicAddressReport::GetPostalCode](https://go.microsoft.com/fwlink/p/?linkid=157842)">ICivicAddressReport::GetPostalCode</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157844" data-raw-source="[LocationDisp.DispCivicAddressReport.PostalCode](https://go.microsoft.com/fwlink/p/?linkid=157844)">LocationDisp.DispCivicAddressReport.PostalCode</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_STATE_PROVINCE</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157846" data-raw-source="[ICivicAddressReport::GetStateProvince](https://go.microsoft.com/fwlink/p/?linkid=157846)">ICivicAddressReport::GetStateProvince</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157847" data-raw-source="[LocationDisp.DispCivicAddressReport.StateProvince](https://go.microsoft.com/fwlink/p/?linkid=157847)">DispCivicAddressReport の場所</a></p></td>
</tr>
</tbody>
</table>

## <a name="managing-state-transitions"></a>状態遷移の管理

センサードライバーは、いつでもさまざまな状態にすることができます。 センサーの状態は、 [**Sensorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)列挙体によって定義されます。 Location API で正常に動作するには、状態遷移を処理するために、次のルールに従う必要があります。

-   状態を初期化する\_は常にセンサー\_状態を開始しますが、起動時に状態変更イベントを発生させません。

-   データが利用可能になったときに、ドライバーはセンサーの\_状態からセンサー\_状態\_準備完了\_に移行する必要があります。
-   ドライバーが最新のデータを報告していない場合は、ドライバーがセンサー\_状態に戻り\_初期化されます。 ドライバーは、移行がいつ発生するかを決定する必要があります。 シグナルが失われても、有効なデータを提供する手段を持っている場合は、センサー\_状態\_準備完了状態のままにします。
-   常に正しい順序でイベントを発生させます。 まず、データが使用可能であることを確認します。 次に、状態変更イベントを発生させます。 最後に、データ更新イベントを発生させます。

-   ドライバーの状態が変化したときに、常に状態変更イベントを発生させます。

-   Location API はセンサーのデータを使用しません。センサー\_状態\_\_データなし、センサー\_状態\_使用できません、センサー\_状態\_エラーです。

次の表では、場所センサードライバーのさまざまなセンサーの状態について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>意味</th>
<th>Location API の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_STATE_READY</p></td>
<td><p>センサードライバーは、完全で正確なデータを持つ新しい場所レポートを提供できます。</p>
<p>たとえば、Wi-fi または携帯電話会社は、接続されて動作しているか、GPS センサーに修正があります。</p>
<p>三通貨センサーのデータを使用して場所を決定する GPS ドライバーは、この状態になります。</p></td>
<td><p>REPORT_RUNNING</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_INITIALIZING</p></td>
<td><p>センサードライバーが修正プログラムを取得しようとしています。 修正プログラムがロックおよび追跡された後、センサードライバーはこの状態を SENSOR_STATE_READY に移行する必要があります。</p>
<p>たとえば、Wi-fi プロバイダーがインターネット接続を探している場合、携帯電話会社が無線を探している場合、GPS センサーが修正プログラムを取得している場合などです。</p>
<p>GPS センサーは、修正プログラムを再取得しようとすると、この状態に再入力する必要があります。</p></td>
<td><p>REPORT_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_NO_DATA</p></td>
<td><p>場所プロバイダーは使用できますが、場所データを提供できません。</p>
<p>たとえば、Wi-fi プロバイダーはインターネットにアクセスできますが、データベースには場所データがありません。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_NOT_AVAILABLE</p></td>
<td><p>場所プロバイダーがデータを取得するために使用する機能が無効になっています。</p>
<p>ラジオがオフになっている場合、GPS センサーがこの状態になることがあります。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_ERROR</p></td>
<td><p>センサーで重大なエラーが発生しました。 センサーはこの状態から回復できますが、回復用の時間枠は不明です。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
</tbody>
</table>

 

次の図は、位置センサーで状態遷移がどのように発生するかを示しています。![状態遷移](images/gps-state-transitions.png)

## <a name="raising-data-updated-and-state-changed-events"></a>データ更新イベントと状態変更イベントの発生

Location API では、データおよび状態変更情報を提供するイベントを発生させるために、GPS センサーなどの位置センサーが必要です。 センサーイベントの発生の詳細については、「[センサードライバーイベントについ](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-driver-events)て」を参照してください。

これらのイベントが発生した場合、ロケーションドライバは次のルールに従う必要があります。

-   センサークラス拡張の[**ISensorClassExtension::P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)メソッドを呼び出して、状態変更イベントを発生させます。 状態変更イベントを発生させるために[**Postevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)を呼び出さないでください。

-   [**Postevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)を呼び出して、データ更新イベントを発生させます。
-   データが最新で正確である場合にのみ、データ更新イベントを発生させます。

-   データ更新イベントを2回発生させないでください。 つまり、キャッシュされたデータを使用してデータ更新イベントを発生させることはできません。 データの同期要求に応答して、キャッシュされたデータを提供できます。

-   イベントを使用して緯度/経度レポートを送信する場合は、常に必要なすべてのデータフィールドを含めます。

-   センサーの精度が変化したときに常にデータ更新イベントを発生させます。

-   センサー\_データ\_種類\_エラー\_RADIUS\_メーターを報告してから、イベントを発生させるか、センサー\_プロパティの値をセンサー\_状態\_準備完了に変更します。

-   不完全なデータレポートは提供しないでください。

-   GPS センサーの修正が失われた場合など、必要なデータフィールドの最新のデータがない可能性があります。 この場合は、センサー\_データ\_TYPE\_NMEA\_文など、拡張データフィールドの更新に関する通知を提供することもできます。 このような通知を提供するには、カスタムイベントの種類を使用し、必要なデータフィールドのデータが使用可能になるまでカスタムイベントのみを発生させる必要があります。 カスタム型を定義する方法の詳細については、「[定数のカスタム値の定義](https://docs.microsoft.com/windows-hardware/drivers/sensors/defining-custom-values-for-constants)」を参照してください。

## <a name="related-topics"></a>関連トピック

[電源とパフォーマンスに関する場所ドライバーのガイドライン](location-driver-guidelines-for-power-and-performance.md)  
