---
title: デバイスのプロパティのサポート
description: デバイスのプロパティのサポート
ms.assetid: ED9A67C4-DFD6-4CF1-B911-29570B3409A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07792c72589abd9cc292b4c9d777a34ff4ce449b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572075"
---
# <a name="support-for-device-properties"></a>デバイスのプロパティのサポート


| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDdi.cpp           | CSensorDdi           |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows のセンサー プラットフォームには、センサーのプロパティの 3 つのカテゴリがサポートされています。

カテゴリの説明の一般的なデバイスのプロパティには、さまざまなデバイス モデル、製造元の名前、およびシリアル番号などの文字列が含まれています。 センサーの現在の状態や、最小のレポート間隔の値などのデバイスのデータも表示されます。 このカテゴリのプロパティとは、読み取り専用です。
データ フィールドのプロパティのプロパティごと、センサーのデータ フィールドに適用されることにします。 加速度計、最小、最大、および各軸の解像度これらです。 このカテゴリのプロパティは読み取り専用です。
設定可能なデバイスのプロパティ、アプリケーションを設定できるプロパティです。 加速度計、これらは、変更の秘密度とレポートの間隔です。
 

ソース ファイル、SensorDdi.cpp の 3 つの配列を持つ**PROPERTYKEY**上の表では、3 つのカテゴリに対応する構造体。

最初の配列には、一般的なセンサーのプロパティ - 製造元の名前、デバイス モデル、およびシリアル番号などの文字列があります。 さらに、最小値と最大範囲、センサーの解像度、および最小のサポートされているレポートの間隔などの値があります。

```cpp
const PROPERTYKEY g_SupportedAccelerometerProperties[] =
{
    WPD_OBJECT_ID,
    SENSOR_PROPERTY_TYPE,
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,
    SENSOR_PROPERTY_MANUFACTURER,
    SENSOR_PROPERTY_MODEL,
    SENSOR_PROPERTY_SERIAL_NUMBER,
    SENSOR_PROPERTY_FRIENDLY_NAME,
    SENSOR_PROPERTY_DESCRIPTION,
    SENSOR_PROPERTY_CONNECTION_TYPE,
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
    SENSOR_PROPERTY_STATE,
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

2 番目の配列には、データ フィールドのプロパティ - 最小値と最大範囲ほか、センサーの解像度ごとに 3 つがあります。

```cpp
const PROPERTYKEY g_SupportedPerDataFieldProperties[] =
{
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
};
```

3 番目の配列には、加速度計の感度の変更と現在のレポート間隔が含まれています。

```cpp
const PROPERTYKEY g_SettableAccelerometerProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,
};
```

## <a name="setting-the-general-and-per-data-field-properties"></a>[全般] の設定およびごとのデータ フィールドのプロパティ

ドライバーのサンプルは、[全般] を設定およびごとの初期化フェーズ中にデータ フィールドのプロパティ。 この作業を処理するコードがある、 **CAccelerometerDevice::SetDefaultProperties**メソッド。 これらのプロパティを設定する呼び出しのシーケンスについては、次を参照してください。[ドライバーの初期化](driver-initialization.md)します。

## <a name="setting-the-writeable-properties"></a>書き込み可能なプロパティの設定

デスクトップ、または WinRT の場合は、アプリ設定のレポート期間、または、センサー クラスの拡張機能の感度の変更プロパティでは、この一連のメソッドを使用して、更新プログラム。

| メソッド                                    | オブジェクトまたはメソッドの呼び出し         | 説明                                                                          |
|-------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------|
| **CSensorDdi::OnSetProperties**           | SensorsClassExtension.dll        | クラスの拡張機能は、プロパティの更新を開始するには、このメソッドを呼び出します。                |
| **CSensorDevice::SetProperties**          | **CSensorDdi::OnSetProperties**  | プロパティのキーと、アプリによって提供される値を使用して、新しいプロパティを適用します。       |
| **CSensorDevice::ApplyUpdatedProperties** | **CSensorDevice::SetProperties** | ドライバーが格納されている最小値が変更がある可能性があるために、新しい値を再適用されます。 |

 

 

 




