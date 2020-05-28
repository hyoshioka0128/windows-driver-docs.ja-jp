---
title: Windows 8.1 用位置センサー ドライバーの作成
description: Windows 8.1 用位置センサー ドライバーの作成
ms.assetid: 18852282-6529-4934-a448-b699e01987de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9a7ad93d66cd087d1780d60e31e6a9540d6e724
ms.sourcegitcommit: 5273e44c5c6c1c87952d74e95e5473c32a916d10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84122700"
---
# <a name="writing-a-location-sensor-driver-for-windows-81"></a>Windows 8.1 用位置センサー ドライバーの作成

ここでは、場所データを提供するデバイス用のドライバーの作成に関する具体的なガイダンスを提供します。 このセクションに記載されている情報に加えて、場所ドライバーの作成者は、「[センサーデバイスドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/sensors/writing-a-sensor-device-driver)」に記載されている情報を理解し、適用する必要があります。

センサーと場所のプラットフォームには、ソフトウェア開発者がプログラムに場所の機能を簡単に追加できるようにするための Windows Location API が用意されています。 場所センサー用のドライバーを作成する場合は、ドライバーを Location API と互換性があるかどうかを理解し、「場所ドライバーのガイドライン」のガイドラインに従って[電源とパフォーマンスを](location-driver-guidelines-for-power-and-performance.md)確保する必要があります。

## <a name="windows-hardware-certification-program-requirements"></a>Windows ハードウェア認定プログラムの要件

Windows ハードウェア認定プログラムを使用すると、ハードウェアの製造元は、デバイスが Windows を操作するために必要な標準を満たしていることを証明する認定を受けることができます。 認定プログラムでは、センサーの場所やセンサーの種類の要件について説明します。 場所センサードライバーをすべての認定プログラムの要件に準拠させる必要があります。 次の要件があります。

- 場所センサーは、必要なデータとセンサーのプロパティのセットをサポートしている必要があります。

- 場所センサーでは、少なくとも1つの組み込みデータレポートの種類に必要なデータフィールドがサポートされている必要があります。

一般に、この WDK ドキュメントに記載されている推奨事項は、認定プログラムの要件と一致します。 ただし、承認のために送信するセンサードライバーを作成する場合は、公式の認定プログラムに関するドキュメントを確認する必要があります。 Windows ハードウェア認定プログラムの詳細については、 [Windows Hardware Developer Central](https://developer.microsoft.com/windows/hardware)の web サイトを参照してください。

## <a name="location-api-requirements"></a>Location API の要件

センサーの他のカテゴリと同じドライバーモデルとクラス拡張を使用して、場所センサー用のドライバーを作成します。 場所センサーとして機能するためには、少なくとも次のものが必要です。

- Location カテゴリに属する場所センサーを特定します。

- センサーの種類を、いずれかの場所センサーの種類に設定します。

- センサーが提供する場所レポートデータフィールドを特定します。

- 必須プロパティをサポートします。

- 要求されたときにデータを提供します。

- 状態遷移を管理します。

- データ更新イベントと状態変更イベントを発生させます。

このセクションの残りの部分では、これらの最小要件について説明します。

## <a name="identifying-the-category"></a>カテゴリを識別する

[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を通じて呼び出された場合は、 **WPD \_ 機能 \_ オブジェクト \_ カテゴリ**のプロパティ値を**センサーカテゴリの \_ \_ 場所**に設定します。 次のコード例は、pValues という名前の[Iportabledevicevalues](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues)へのポインターを使用して、この定数を設定する方法を示しています。

```cpp
hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, SENSOR_CATEGORY_LOCATION);
```

## <a name="setting-the-location-sensor-type"></a>場所センサーの種類の設定

[**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)を通じて呼び出された場合は、**センサー \_ プロパティの \_ TYPE**プロパティの値を正しい値に設定します。 次のコード例は、pValues という名前の[Iportabledevicevalues](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues)へのポインターを使用してセンサーの種類を設定する方法を示しています。 ** \_ \_ \_ **

```cpp
hr = pValues->SetGuidValue(SENSOR_PROPERTY_TYPE, SENSOR_TYPE_LOCATION_GPS);
```

## <a name="identifying-the-supported-data-fields"></a>サポートされるデータフィールドの特定

Location API は、2種類の場所レポートを定義します。 これらは、場所データを編成するオブジェクトです。 LatLong レポートには、緯度、経度、および標高のデータフィールドと、エラー範囲情報を含むデータフィールドが含まれています。 都市の住所レポートには、市区町村や郵便番号などの番地のデータフィールドが含まれています。 この2つのデータレポートの種類の少なくとも1つについて、場所ドライバーが必要なデータフィールドをサポートしている必要があります。

LatLong レポートをサポートするには、次のデータフィールドが必要です。

- センサー \_ データ \_ 型 \_ 緯度 \_ 度

- センサー \_ データ \_ 型 \_ 経度 \_ 度

- センサー \_ データ \_ 型の \_ エラー \_ 半径 \_ メーター

都市の住所レポートをサポートするには、次のデータフィールドの少なくとも1つが必要です。

- センサー \_ データ \_ 型 \_ COUNTRY \_ REGION

プラットフォームで定義された場所のデータフィールドの完全なセットを表示するには、「 [Windows センサーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」セクションの「[**センサー \_ カテゴリの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-category-loc)」を参照してください。

[**ISensorDriver:: OnGetSupportedDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)を通じて呼び出された場合、サポートされるデータフィールドプロパティのキー定数を[Iportabledevicekeycollection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection)に追加します。これは、 *ppsupporteddatafields*パラメーターを通じて返されます。 次のコード例では、pKeyCollection という変数を使用して、郵便番号データフィールドを[Iportabledevicekeycollection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection)に追加する方法を示します。

```cpp
pKeyCollection->Add(SENSOR_DATA_TYPE_POSTALCODE);
```

## <a name="support-the-required-properties"></a>必須プロパティをサポートする

他のセンサードライバーと同様に、場所ドライバーは一連のプロパティを使用してセンサー自体に関する情報を提供します。 Windows ハードウェア認定プログラムでは、場所センサーがサポートする必要があるプロパティの最小セットを指定します。 センサーのプロパティとその意味、およびセンサードライバーに必要なプロパティの詳細については、「[**センサーのプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)」を参照してください。 次の一覧には、必要なプロパティが含まれています。

- WPD \_ 機能 \_ オブジェクト \_ カテゴリ

- センサーの \_ プロパティの \_ 種類

- センサーの \_ プロパティの \_ 状態

- センサー \_ プロパティの \_ 永続的な \_ 一意 \_ ID

- センサーの \_ プロパティの \_ 製造元

- センサーの \_ プロパティ \_ モデル

- センサーの \_ プロパティの \_ シリアル \_ 番号

- センサー \_ プロパティの \_ フレンドリ \_ 名

- センサー \_ プロパティの \_ 最小 \_ レポート \_ 間隔

- センサー \_ プロパティ \_ の現在の \_ レポート \_ 間隔

- センサー \_ プロパティの \_ 場所の必要な \_ \_ 精度

## <a name="providing-data"></a>データの提供

場所ドライバーは、他のセンサードライバーと同じメカニズムを使用してデータを提供します。 つまり、センサークラス拡張は[**ISensorDriver:: OnGetDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)を使用してドライバーを呼び出し、ドライバーは*ppdatavalues*パラメーターを使用して値を返します。

次の要件は、場所センサーからデータを提供する場合に適用されます。

- 同期要求を使用してデータを提供し、[イベントを発生](https://docs.microsoft.com/windows-hardware/drivers/sensors/raising-events)させます。

- 最新のデータレポートのコピーを保持します。 要求時に新しいデータを使用できない場合は、キャッシュされたレポートを返します。 タイムスタンプは更新しないでください。

- センサー \_ データ \_ 型の \_ 緯度 \_ 度とセンサーデータ型の値 \_ は \_ \_ \_ 、実際の緯度と経度の範囲外になるように指定しないでください。

- センサー \_ データ \_ 型のエラー半径メーターの値を0以下で報告しないで \_ \_ \_ ください。

- センサー \_ データ型の国の \_ 地域の値を、 \_ \_ 有効な ISO 3166 1-alpha-2 国コードに設定します。

- ドライバーが緯度/経度と都市の両方の住所レポートをサポートしている場合、これらのレポートの場所データは、同じ物理的な場所に対応している必要があります。

次の表では、Location API データレポートフィールドに対応する[センサーデータフィールド](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-categories--types--and-data-fields)について説明します。 場所のデータレポートを提供するときに、これらのデータフィールド定数を使用します。

| センサー定数 | Location API メソッドとプロパティ |
| --- | --- |
| SENSOR_DATA_TYPE_ADDRESS1 | [ICivicAddressReport::GetAddressLine1](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getaddressline1)<br><br>[DispCivicAddressReport. AddressLine1](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-addressline1) |
| SENSOR_DATA_TYPE_ADDRESS2 | [ICivicAddressReport::GetAddressLine2](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getaddressline2)<br><br>[DispCivicAddressReport. AddressLine2](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-addressline2) |
| SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS | [ILatLongReport:: GetAltitudeError](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getaltitudeerror)<br><br>[DispLatLongReport. AltitudeError](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-altitudeerror) |
| SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS | [ILatLongReport:: GetAltitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getaltitude)<br><br>[LocationDisp](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-altitude) |
| SENSOR_DATA_TYPE_CITY | [ICivicAddressReport:: GetCity](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getcity)<br><br>[DispCivicAddressReport. 市区町村](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-city)<br><br>[Windows. CivicAddress](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City) |
| SENSOR_DATA_TYPE_COUNTRY_REGION | [ICivicAddressReport:: GetCountryRegion](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getcountryregion)<br><br>[LocationDisp](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-civicaddressreport-countryregion) |
| SENSOR_DATA_TYPE_ERROR_RADIUS_METERS | [ILatLongReport:: GetErrorRadius](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-geterrorradius)<br><br>[DispLatLongReport. ErrorRadius](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-errorradius) |
| SENSOR_DATA_TYPE_LATITUDE_DEGREES | [ILatLongReport:: GetLatitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getlatitude)<br><br>[LocationDisp](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-latitude) |
| SENSOR_DATA_TYPE_LONGITUDE_DEGREES | [ILatLongReport:: GetLongitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getlongitude)<br><br>[LocationDisp](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-longitude) |
| SENSOR_DATA_TYPE_POSTALCODE | [ICivicAddressReport:: GetPostalCode 番号](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getpostalcode)<br><br>[LocationDisp](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-postalcode) |
| SENSOR_DATA_TYPE_STATE_PROVINCE | [ICivicAddressReport:: GetStateProvince](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getstateprovince)<br><br>[DispCivicAddressReport の場所](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-stateprovince) |

## <a name="managing-state-transitions"></a>状態遷移の管理

センサードライバーは、いつでもさまざまな状態にすることができます。 センサーの状態は、 [**Sensorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)列挙体によって定義されます。 Location API で正常に動作するには、状態遷移を処理するために、次のルールに従う必要があります。

- 常にセンサー状態の初期化中に開始 \_ \_ しますが、起動時に状態変更イベントは発生しません。

- \_ \_ \_ \_ データが使用可能な場合、ドライバーはセンサー状態からセンサー状態に移行する必要があります。

- ドライバーが \_ \_ 最新のデータを報告していない場合は、ドライバーを初期化してセンサー状態に戻す必要があります。 ドライバーは、移行がいつ発生するかを決定する必要があります。 シグナルが失われても、有効なデータを提供する手段を持っている場合は、センサー \_ 状態の \_ 準備完了状態を維持します。

- 常に正しい順序でイベントを発生させます。 まず、データが使用可能であることを確認します。 次に、状態変更イベントを発生させます。 最後に、データ更新イベントを発生させます。

- ドライバーの状態が変化したときに、常に状態変更イベントを発生させます。

-Location API は、センサーの状態が " \_ \_ データなし" \_ 、"センサーの状態は \_ \_ 使用できません" \_ 、"センサーの \_ 状態" \_ エラーの状態にあるセンサーのデータを使用しません。

次の表では、場所センサードライバーのさまざまなセンサーの状態について説明します。

| 値 | 説明 | Location API の状態 |
| --- | --- | --- |
| SENSOR_STATE_READY | センサードライバーは、完全で正確なデータを持つ新しい場所レポートを提供できます。<br><br>たとえば、Wi-fi または携帯電話会社は、接続されて動作しているか、GPS センサーに修正があります。<br><br>三通貨センサーのデータを使用して場所を決定する GPS ドライバーは、この状態になります。 | REPORT_RUNNING |  
| SENSOR_STATE_INITIALIZING | センサードライバーが修正プログラムを取得しようとしています。 修正プログラムがロックおよび追跡された後、センサードライバーはこの状態を SENSOR_STATE_READY に移行する必要があります。<br><br>たとえば、Wi-fi プロバイダーがインターネット接続を探している場合、携帯電話会社が無線を探している場合、GPS センサーが修正プログラムを取得している場合などです。<br><br>GPS センサーは、修正プログラムを再取得しようとすると、この状態に再入力する必要があります。 | REPORT_INITIALIZING |  
| SENSOR_STATE_NO_DATA | 場所プロバイダーは使用できますが、場所データを提供できません。<br><br>たとえば、Wi-fi プロバイダーはインターネットにアクセスできますが、データベースには場所データがありません。 | REPORT_ERROR |  
| SENSOR_STATE_NOT_AVAILABLE | 場所プロバイダーがデータを取得するために使用する機能が無効になっています。<br><br>ラジオがオフになっている場合、GPS センサーがこの状態になることがあります。 | REPORT_ERROR |  
| SENSOR_STATE_ERROR | センサーで重大なエラーが発生しました。 センサーはこの状態から回復できますが、回復用の時間枠は不明です。 | REPORT_ERROR |  

次の図は、位置センサーで状態遷移がどのように発生するかを示しています。![状態遷移](images/gps-state-transitions.png)

## <a name="raising-data-updated-and-state-changed-events"></a>データ更新イベントと状態変更イベントの発生

Location API では、データおよび状態変更情報を提供するイベントを発生させるために、GPS センサーなどの位置センサーが必要です。 センサーイベントの発生の詳細については、「[センサードライバーイベントについ](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-driver-events)て」を参照してください。

これらのイベントが発生した場合、ロケーションドライバは次のルールに従う必要があります。

- センサークラス拡張の[**ISensorClassExtension::P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)メソッドを呼び出して、状態変更イベントを発生させます。 状態変更イベントを発生させるために[**Postevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)を呼び出さないでください。

- [**Postevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)を呼び出して、データ更新イベントを発生させます。

- データが最新で正確である場合にのみ、データ更新イベントを発生させます。

- データ更新イベントを2回発生させないでください。 つまり、キャッシュされたデータを使用してデータ更新イベントを発生させることはできません。 データの同期要求に応答して、キャッシュされたデータを提供できます。

- イベントを使用して緯度/経度レポートを送信する場合は、常に必要なすべてのデータフィールドを含めます。

- センサーの精度が変化したときに常にデータ更新イベントを発生させます。

- センサーデータ型のエラー半径メーターの有効な値を報告 \_ してから、イベントを発生さ \_ \_ \_ \_ せるか、センサーの \_ プロパティ状態の値 \_ をセンサー状態に変更 \_ \_ します。

- 不完全なデータレポートは提供しないでください。

- GPS センサーの修正が失われた場合など、必要なデータフィールドの最新のデータがない可能性があります。 この場合でも、センサー \_ データ型 NMEA 文などの拡張データフィールドの更新に関する通知を提供する必要があり \_ \_ \_ ます。 このような通知を提供するには、カスタムイベントの種類を使用し、必要なデータフィールドのデータが使用可能になるまでカスタムイベントのみを発生させる必要があります。 カスタム型を定義する方法の詳細については、「[定数のカスタム値の定義](https://docs.microsoft.com/windows-hardware/drivers/sensors/defining-custom-values-for-constants)」を参照してください。

## <a name="related-topics"></a>関連トピック

[電源とパフォーマンスに関する場所ドライバーのガイドライン](location-driver-guidelines-for-power-and-performance.md)  
