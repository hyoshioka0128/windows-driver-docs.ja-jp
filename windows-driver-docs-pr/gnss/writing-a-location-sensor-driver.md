---
title: Windows 8.1 用位置センサー ドライバーの作成
description: Windows 8.1 用位置センサー ドライバーの作成
ms.assetid: 18852282-6529-4934-a448-b699e01987de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c8d0a8e8015545f12f82bc4fe4e5e01829004f
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419592"
---
# <a name="writing-a-location-sensor-driver-for-windows-81"></a>Windows 8.1 用位置センサー ドライバーの作成

このセクションでは、場所データを提供するデバイス用のドライバーを記述するための具体的なガイダンスを提供します。 このセクションに含まれている情報だけでなく場所ドライバー作成者する必要がありますも理解し、で提供される情報を適用[センサー デバイス ドライバーを作成](https://msdn.microsoft.com/library/windows/hardware/ff545927)です。

Sensor and Location プラットフォームは、自分のプログラムに簡単に場所の機能を追加するソフトウェア開発者を有効にする Windows Location API を提供します。 位置情報センサー用のドライバーを作成する場合は、ドライバーの場所 API 互換性を確保し、ガイドラインに従う方法を理解する必要があります[能力とパフォーマンスのドライバーのガイドラインを場所](location-driver-guidelines-for-power-and-performance.md)します。

## <a name="windows-hardware-certification-program-requirements"></a>Windows ハードウェア認定プログラム要件

Windows ハードウェア認定プログラムには、ハードウェアの製造元を自分のデバイスが Windows を操作するための必要な基準を満たす証明書を受信するができます。 認定プログラムには、場所のセンサーの要件と他の種類のセンサーがについて説明します。 場所センサー ドライバー認定プログラムのすべての要件に準拠する必要があります。 これらの要件を以下に示します。

-   場所のセンサーには、必要な一連のデータとセンサーのプロパティをサポートする必要があります。

-   位置センサーは、少なくとも 1 つの組み込みデータ レポートの種類の必要なデータ フィールドをサポートする必要があります。

一般に、この WDK ドキュメントの推奨事項では、認定プログラムの要件と一致します。 ただし、承認用に送信するセンサー ドライバーを作成するときに、公式の認定プログラムのドキュメントを確認する必要があります。 Windows ハードウェア認定プログラムに関する詳細については、次を参照してください。、 [Windows Hardware Developer Central](https://developer.microsoft.com/en-us/windows/hardware) web サイト。

## <a name="location-api-requirements"></a>API の場所の要件

場所のセンサー用のドライバーを作成するには、センサーの他の任意のカテゴリの場合と同じドライバー モデル、クラス拡張機能を使用します。 少なくとも、位置情報センサーとして動作するドライバーが必要です。

-   場所のカテゴリに属するものとして位置情報センサーを識別します。

-   場所の種類のセンサーのいずれかにセンサーの種類を設定します。

-   センサーは、場所レポートのデータ フィールドを識別します。

-   必要なプロパティをサポートします。

-   要求されたデータを提供します。

-   状態遷移を管理します。

-   データ更新、および状態変更イベントを発生させます。

このセクションの残りの部分は、これらの最小要件を説明します。

## <a name="identifying-the-category"></a>カテゴリを識別します。

呼び出される[ **ISensorDriver::OnGetProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545610)、設定、 **WPD\_機能\_オブジェクト\_カテゴリ**プロパティの値を**センサー\_カテゴリ\_場所**します。 次のコード例は、この定数へのポインターを設定する方法を示しています。 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486) pValues という名前です。

```cpp
hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, SENSOR_CATEGORY_LOCATION);
```

## <a name="setting-the-location-sensor-type"></a>場所のセンサーの種類の設定

呼び出される[ **ISensorDriver::OnGetProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545610)、設定、**センサー\_プロパティ\_型**プロパティの値は、正しい値。 次のコード例を使用して、センサーの種類を設定する方法を示しています、**センサー\_型\_場所\_GPS**へのポインターを通じて一定[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)pValues という名前です。

```cpp
hr = pValues->SetGuidValue(SENSOR_PROPERTY_TYPE, SENSOR_TYPE_LOCATION_GPS);
```

## <a name="identifying-the-supported-data-fields"></a>サポートされているデータ フィールドを識別します。

Location API は、2 種類のレポートの場所を定義します。 これらは、場所データを整理するオブジェクトです。 LatLong レポートには、緯度、経度、および範囲のエラー情報が含まれているデータ フィールドと共に、高度のデータ フィールドが含まれます。 都市の住所のレポートには、市区町村や郵便番号などの住所データ フィールドが含まれます。 場所は、ドライバーは、これら 2 つのデータのレポートの種類の少なくとも 1 つの必要なデータ フィールドをサポートする必要があります。

LatLong レポートをサポートするためには、次のデータ フィールドが必要です。

-   センサー\_データ\_型\_緯度\_度
-   センサー\_データ\_型\_経度\_度
-   センサー\_データ\_型\_エラー\_RADIUS\_のメーター

都市の住所のレポートをサポートするために、次のデータ フィールドの少なくとも 1 つが必要です。

-   センサー\_データ\_型\_国\_リージョン

(プラットフォームで定義された場所のデータ フィールドの完全なセットを表示するのを参照してください[**センサー\_カテゴリ\_場所**](https://msdn.microsoft.com/library/windows/hardware/dn265186)で、 [Windows センサー参照](https://msdn.microsoft.com/library/windows/hardware/ff545907)。セクションです)。

呼び出すとき[ **ISensorDriver::OnGetSupportedDataFields**](https://msdn.microsoft.com/library/windows/hardware/ff545620)にサポートされているデータ フィールド プロパティ キー定数を追加、 [IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)を返す、 *ppSupportedDataFields*パラメーター。 次のコード例は、郵便番号のデータ フィールドを追加する方法を示しています。 [IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484) pKeyCollection という名前の変数を使用します。

```cpp
pKeyCollection->Add(SENSOR_DATA_TYPE_POSTALCODE);
```

## <a name="support-the-required-properties"></a>必要なプロパティをサポートします。

その他のセンサー ドライバーのようには、場所ドライバーは、一連のプロパティのセンサー自体に関する情報を提供します。 Windows ハードウェア認定プログラムでは、最低限必要な一連の位置情報センサーをサポートする必要がありますプロパティを指定します。 センサーのプロパティ、その意味、およびプロパティは、センサー ドライバーに必要な詳細については、次を参照してください。 [**センサー プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff545859)します。 次の一覧には、必要なプロパティが含まれています。

-   WPD\_機能\_オブジェクト\_カテゴリ

-   センサー\_プロパティ\_型

-   センサー\_プロパティ\_状態

-   センサー\_プロパティ\_持続\_UNIQUE\_ID

-   センサー\_プロパティ\_製造元

-   センサー\_プロパティ\_モデル

-   センサー\_プロパティ\_シリアル\_数

-   センサー\_プロパティ\_フレンドリ\_名

-   センサー\_プロパティ\_MIN\_レポート\_間隔

-   センサー\_プロパティ\_現在\_レポート\_間隔

-   センサー\_プロパティ\_場所\_DESIRED\_精度

## <a name="providing-data"></a>データを提供します。

ドライバーの場所は、他センサー ドライバーと同じメカニズムを通じてデータを提供します。 センサー クラスの拡張機能のドライバーは、呼び出しは、 [ **ISensorDriver::OnGetDataFields** ](https://msdn.microsoft.com/library/windows/hardware/ff545607)し、ドライバーによって値を返します、 *ppDataValues*パラメーター。

位置情報センサーからデータを提供するために、次の要件が適用されます。

-   同期要求を使用し、両方のデータを提供[イベントを発生させる](https://msdn.microsoft.com/library/windows/hardware/ff545695)します。

-   最新のデータのレポートのコピーを保持します。 要求するときに新しいデータが利用できない場合は、キャッシュされたレポートを返します。 タイムスタンプは更新されません。

-   センサーの値を指定しない\_データ\_型\_緯度\_度とセンサー\_データ\_型\_経度\_外度、実際の緯度と経度の範囲です。

-   センサーの値を報告しない\_データ\_型\_エラー\_RADIUS\_が 0 以下のメーターです。

-   センサーの値を設定\_データ\_型\_国\_有効な ISO 3166 1-alpha-2 国別コード領域。

-   ドライバーは、緯度/経度と都市の住所のレポートの両方をサポートする場合、これらのレポート内の場所のデータは物理的に同じ場所に対応します。

次の表、[センサー データ フィールド](https://msdn.microsoft.com/library/windows/hardware/ff545718)Location API データ レポートのフィールドに対応しています。 場所のデータのレポートを提供する場合は、これらのデータ フィールドの定数を使用します。

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
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157830" data-raw-source="[LocationDisp.DispCivicAddressReport.City](https://go.microsoft.com/fwlink/p/?linkid=157830)">LocationDisp.DispCivicAddressReport.City</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/windows.devices.geolocation.civicaddress.city.aspx" data-raw-source="[Windows.Devices. Geolocation.CivicAddress](https://msdn.microsoft.com/library/windows/apps/windows.devices.geolocation.civicaddress.city.aspx)">含まれる windows devices です。Geolocation.CivicAddress</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157831" data-raw-source="[ICivicAddressReport::GetCountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157831)">ICivicAddressReport::GetCountryRegion</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157832" data-raw-source="[LocationDisp.DispCivicAddressReport.CountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157832)">LocationDisp.DispCivicAddressReport.CountryRegion</a></p></td>
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
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157847" data-raw-source="[LocationDisp.DispCivicAddressReport.StateProvince](https://go.microsoft.com/fwlink/p/?linkid=157847)">LocationDisp.DispCivicAddressReport.StateProvince</a></p></td>
</tr>
</tbody>
</table>

## <a name="managing-state-transitions"></a>状態遷移の管理

いつでもでも、状態の数のいずれかでセンサー ドライバーができます。 センサーの状態がによって定義されている、 [ **SensorState** ](https://msdn.microsoft.com/library/windows/hardware/ff545708)列挙体。 Location API を正常に機能するには、場所のセンサーは状態遷移を処理するため、これらの規則に従う必要があります。

-   センサーでは常にスタート\_状態\_の状態を初期化していますが、起動時に状態変更イベントを発生させません。

-   ドライバーは、センサーから移行する必要があります\_状態\_センサーを初期化\_状態\_データが使用可能な場合を準備します。
-   ドライバーがセンサーに移行する必要があります\_状態\_ドライバーにレポートを現在のデータがあるない場合に初期化しています。 ドライバーは、その遷移が発生したときを決める必要があります。 センサーでは常に、シグナルが失われている有効なデータを提供するための手段がまだある場合は、\_状態\_準備完了状態。
-   常に正しい順序でのイベントを発生させます。 最初に、データが使用できることを確立します。 次に、状態変更イベントを発生します。 最後に、データ更新イベントが発生します。

-   常に、ドライバーの状態が変更されたときの状態変更イベントを発生します。

-   Location API では、次の状態で、センサーからのデータは使用しません。センサー\_状態\_いいえ\_データ、センサー\_状態\_いない\_利用可能なセンサー\_状態\_エラー。

場所のセンサー ドライバーのさまざまなセンサーの状態は次の表で説明されている.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
<th>API の場所の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_STATE_READY</p></td>
<td><p>センサー ドライバーでは、完全かつ正確なデータを格納している場所の新しいレポートを提供できます。</p>
<p>たとえば、Wi-fi または携帯電話のプロバイダーが接続され、作業、または、GPS センサーが修正。</p>
<p>場所を特定する三角測量センサーからのデータが使用した GPS ドライバーでは、この状態があります。</p></td>
<td><p>REPORT_RUNNING</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_INITIALIZING</p></td>
<td><p>センサー ドライバーは、修正プログラムを取得しようとしています。 センサー ドライバー SENSOR_STATE_READY、修正プログラムがロックされた後と追跡への移行にこの状態のままにする必要があります。</p>
<p>たとえば、Wi-fi プロバイダーは、インターネット接続を探して、無線、携帯電話のプロバイダーが検索または GPS センサーが修正プログラムを取得します。</p>
<p>修正プログラムを再取得しようとすると、GPS センサーはこの状態を再入力する必要があります。</p></td>
<td><p>REPORT_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_NO_DATA</p></td>
<td><p>場所プロバイダーが使用できるが、場所データを提供することはありません。</p>
<p>たとえば、Wi-fi プロバイダーが、インターネットへのアクセスが、データベースの場所データがありません。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_NOT_AVAILABLE</p></td>
<td><p>場所プロバイダーを使用してデータを取得する機能は無効です。</p>
<p>GPS センサーは、オプションがになっている場合、この状態である可能性があります。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_ERROR</p></td>
<td><p>センサー、主要なエラーが発生しました。 センサーは、この状態から回復できますが、回復の時間枠は認識されていません。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
</tbody>
</table>

 

次の図は、位置情報センサーの状態遷移が発生する方法を示します。![状態遷移](images/gps-state-transitions.png)

## <a name="raising-data-updated-and-state-changed-events"></a>データ更新、および状態変更イベントを発生させる

Location API、データと状態変更情報を提供するイベントを発生させる、GPS センサーなどの場所のセンサーが必要です。 センサーのイベントの発生に関する詳細については、次を参照してください。[センサー ドライバー イベントについて](https://msdn.microsoft.com/library/windows/hardware/ff545385)します。

これらのイベントを発生させる場合ドライバーの場所はこれらの規則に従う必要があります。

-   センサー クラスの拡張を呼び出して、状態変更イベントを発生させる[ **ISensorClassExtension::PostStateChange** ](https://msdn.microsoft.com/library/windows/hardware/ff545523)メソッド。 呼び出さない[ **PostEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff545519)状態変更イベントを発生させます。

-   呼び出して、データ更新後のイベントを発生させる[ **PostEvent**](https://msdn.microsoft.com/library/windows/hardware/ff545519)します。
-   データが最新かつ正確な場合にのみ、データ更新イベントを発生します。

-   2 回、データ更新イベントを発生しません。 これは、キャッシュされたデータを使用してデータ更新イベントを発生させるしないことを意味します。 データの同期要求への応答でキャッシュされたデータを行うことができます。

-   イベントを使用して緯度/経度レポートを送信するときに常にすべての必要なデータ フィールドが含まれます。

-   センサーの精度が変更されたときに、データ更新イベントが常に発生します。

-   センサーの有効な値をレポート\_データ\_型\_エラー\_RADIUS\_メーターのイベントの発生またはセンサーの値を変更する前に\_プロパティ\_センサーの状態\_状態\_準備ができています。

-   不完全なデータのレポートは提供されません。

-   GPS センサーがその修正を失ったときなど、必要なデータ フィールドの現在のデータができないことがあります。 この場合、センサーなどの拡張データ フィールドの更新に関する通知を提供する可能性がありますも\_データ\_型\_NMEA\_文。 このような通知を提供するにはカスタム イベントの種類を使用して、必要なデータ フィールドのデータが使用可能になるまでのカスタム イベントのみが発生します。 カスタム型を定義する方法については、次を参照してください。[定数のカスタム値を定義する](https://msdn.microsoft.com/library/windows/hardware/ff545437)します。

## <a name="related-topics"></a>関連トピック

[能力とパフォーマンスの場所のドライバーのガイドライン](location-driver-guidelines-for-power-and-performance.md)  
