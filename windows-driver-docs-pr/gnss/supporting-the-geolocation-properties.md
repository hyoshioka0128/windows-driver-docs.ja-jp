---
title: 位置情報プロパティのサポート
description: ソース ファイル、geolocation.cpp、シミュレートされたセンサーでサポートされるプロパティを定義する PROPERTYKEY 構造体の 3 つの配列が含まれています。
ms.assetid: 0D25D58F-1023-4470-9F7D-E62544B87A42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad9b294e3e67228b98d2022019ba8194c89e7145
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326180"
---
# <a name="supporting-the-geolocation-properties"></a>位置情報プロパティのサポート

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

ソース ファイル、geolocation.cpp、シミュレートされたセンサーでサポートされるプロパティを定義する PROPERTYKEY 構造体の 3 つの配列が含まれています。

最初の配列では、シミュレートされたセンサーでサポートされる読み取り専用と読み取り/書き込みプロパティを定義します。

```cpp
const PROPERTYKEY g_SupportedGeolocationProperties[] =
{
    SENSOR_PROPERTY_TYPE,                       //[VT_CLSID]
    SENSOR_PROPERTY_STATE,                      //[VT_UI4]
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,        //[VT_UI4]
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,       //[VT_CLSID]
    SENSOR_PROPERTY_MANUFACTURER,               //[VT_LPWSTR]
    SENSOR_PROPERTY_MODEL,                      //[VT_LPWSTR]
    SENSOR_PROPERTY_SERIAL_NUMBER,              //[VT_LPWSTR]
    SENSOR_PROPERTY_FRIENDLY_NAME,              //[VT_LPWSTR]
    SENSOR_PROPERTY_DESCRIPTION,                //[VT_LPWSTR]
    SENSOR_PROPERTY_CONNECTION_TYPE,            //[VT_UI4]
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
    WPD_FUNCTIONAL_OBJECT_CATEGORY,             //[VT_CLSID]
};
```

ドライバーのサンプルではこれらの値プロパティ (またはプロパティ) を取得するときにアプリケーションの要求に応答します。 プロパティの値を取得する方法は、 **CGeolocation::GetPropertyValuesForGeolocationObject**します。

2 番目の配列では、省略可能なプロパティを定義します。

```cpp
const PROPERTYKEY g_OptionalSupportedGeolocationProperties[] =
{
    SENSOR_PROPERTY_RANGE_MAXIMUM,              //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_RANGE_MINIMUM,              //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_ACCURACY,                   //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_RESOLUTION,                 //[VT_UNKNOWN], IPortableDeviceValues
};
```

3 番目の配列では、擬似センサーでサポートされている書き込み可能なまたは、設定可能なプロパティを定義します。

```cpp
const PROPERTYKEY g_SettableGeolocationProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
};
```

ドライバーのサンプルは、書き込み可能なプロパティ (またはプロパティ) を更新するときにもこれらの値を使用します。 プロパティ値を更新する方法は、 **CGeolocation::UpdateGeolocationPropertyValues**します。

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](sensors-geolocation-driver-sample.md)  



