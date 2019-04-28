---
title: 位置情報オブジェクトの初期化
description: Geolocation.cpp には、設定可能なプロパティのキーと、シミュレートされた地理的位置情報センサーのデータ フィールドのキーを初期化する Initialize メソッドが含まれています。
ms.assetid: 3803BD3B-9853-4AA4-A278-22F8D835B1ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d43e676a93ec298a0daf71b18820a6f70b72c18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371038"
---
# <a name="initializing-the-geolocation-object"></a>位置情報オブジェクトの初期化

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

オブジェクトのソース ファイル、geolocation.cpp が含まれています、**初期化**設定可能なプロパティのキーと、シミュレートされた地理的位置情報センサーのデータ フィールドのキーを初期化するメソッド。 このメソッドは、起動時にセンサー マネージャーによって呼び出されます。

プロパティのキー (**PROPERTYKEY**) から成るデータ構造を**GUID**と**DWORD**センサー プロパティの一意の識別子を提供します。 シミュレートされた地理的位置情報、センサーの場合は、3 つの設定可能なプロパティ キーに対応する: デバイスの感度の変更、その現在のレポート間隔、および必要な精度。 これらのキーは、ファイル geolocation.cpp で定義されます。

```cpp
const PROPERTYKEY g_SettableGeolocationProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
};
```

感度の変更とレポート期間の詳細についてを参照してください、[データのフィルター処理](https://msdn.microsoft.com/library/windows/hardware/hh706201)トピック。

データ フィールドのキーは、 **PROPERTYKEY**ドライバーがサポートされている各一意のデータ フィールドを識別するために使用します。 擬似の地理的位置情報センサーの場合は、読み取り、現在の緯度 (度単位) で、(度単位) での現在の経度のタイムスタンプなどのデータを含む 8 つのサポートされているデータ フィールド。 これらのキーは、ファイル geolocation.cpp でも定義されます。

```cpp
const PROPERTYKEY g_SupportedGeolocationDataFields[] =
{
    SENSOR_DATA_TYPE_TIMESTAMP,                 //[VT_FILETIME]
    SENSOR_DATA_TYPE_LATITUDE_DEGREES,          //[VT_R8]
    SENSOR_DATA_TYPE_LONGITUDE_DEGREES,         //[VT_R8]
    SENSOR_DATA_TYPE_ERROR_RADIUS_METERS,       //[VT_R8]
    SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS, //[VT_R8]
    SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS, //[VT_R8]
    SENSOR_DATA_TYPE_SPEED_KNOTS,               //[VT_R8]
    SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES,      //[VT_R8]
};
```

**CSensorManager::Start**メソッドを呼び出す**CGeolocation::Initialize**センサー デバイス ドライバー インターフェイス (DDI) が作成された後すぐにします。 この作業は、モジュール sensormanager.cpp で発生します。

**初期化**メソッドをさらに、起動、 **InitializeGeolocation**メソッド。 この後者のメソッドを呼び出す**CGeolocation::AddGeolocationSettablePropertyKeys**擬似センサーでサポートされている書き込み可能なプロパティのプロパティのキーを初期化します。 プロパティのキーを追加した後、 **InitializeGeolocation**メソッドを呼び出す**CGeolocation::AddGeolocationDataFieldKeys**サポートされているデータ フィールドのデータ フィールドのキーを初期化します。

## <a name="related-topics"></a>関連トピック
[地理的位置情報オブジェクトを定義します。](defining-the-geolocation-object.md)  
[データのフィルター処理](https://msdn.microsoft.com/library/windows/hardware/hh706201)  



