---
Description: センサー プロパティの定義
title: センサー プロパティの定義
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36174949ef6b5dd40e0f6b53c3e3270219500af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378663"
---
# <a name="defining-the-sensor-properties"></a>センサー プロパティの定義


Windows ポータブル デバイス (WPD) プロパティは、オブジェクトの説明するメタデータです。 このセクションでは、サンプルのドライバーがサポートするプロパティについて説明します。 デバイス オブジェクトは、18 のプロパティをサポートしているし、センサーの個々 のオブジェクトは、10 個のプロパティをサポートします。 一部のオブジェクト プロパティに WPD などのドライバーの機能に必要な\_オブジェクト\_ID と WPD\_オブジェクト\_持続\_UNIQUE\_id。 WPD などのオブジェクトを記述する情報を提供するその他のプロパティが存在\_デバイス\_製造元。

WDK には、WPD ドライバー開発者向けのいくつかのツールが含まれています。 これらのツールの 1 つ*WpdInfo.exe*開発者がオブジェクトと特定のドライバーによって公開されているプロパティを確認するに使用します。 次のスクリーン ショット、 *WpdInfo.exe*ツールは、ドライバーでデバイス オブジェクトをサポートするプロパティを示します。

![wpd 情報ツール](images/wpdinfo_device_object.png)

前の画像では、上部のウィンドウの左端の列は、ドライバーがサポートするオブジェクトの一覧を表示します。 中央のウィンドウには、デバイス オブジェクトのドライバーがサポートする 18 プロパティが一覧表示します。 このペインの最初の列には、プロパティ名が一覧表示されます、2 番目の列には、そのプロパティの値が一覧表示されます、3 番目の列と型を一覧表示します。 下のウィンドウには、ドライバーをサポートしているイベントによって返される情報が表示されます。

次のスクリーン ショット、 *WpdInfo.exe*ツールは TempHumidity オブジェクトをサポートするプロパティを示します。

![wpd 情報ツール](images/wpdinfo_temphumidity_object.png)

このオブジェクトは、10 個のプロパティをサポートします。 1 つに、センサー\_読み取りとセンサー\_UPDATE\_間隔は WpdBasicHardwareDriver、によって定義され、センサー ファームウェアによって発行されたデータを表現するカスタム プロパティ。 この例では、センサーで\_読み取りプロパティは、センサーを識別します (2 = Sensiron 気温・湿度センサー)、要素の数 (1)、要素のサイズ (バイト単位の 7)、現在の気温 (74.4 F) および相対湿度 (37.3%)。 センサー\_UPDATE\_INTERVAL プロパティは、デバイスがイベントを起動する頻度を指定します。 この値は、02000 は、2 秒の更新間隔を示します (ミリ秒単位) で指定されます。 ファームウェアでは、2 ~ 60 秒間の更新の間隔の構成をサポートします。

WPD では、プロパティが PROPERTYKEY データ構造体によって表されます。 この構造体は、2 つの部分で構成されています: GUID と DWORD。 グローバル一意識別子 (GUID) がプロパティのカテゴリを識別し、dword 値がそのカテゴリ内の特定のプロパティを識別します。 PROPERTYKEY 構造の詳細については、次を参照してください。 [PROPERTYKEYs と WPD で Guid](propertykeys-and-guids-in-windows-portable-devices.md) Windows Driver Kit (WDK) ドキュメントです。

DECLARE を使用して\_PROPERTYKEY のマクロには、ドライバーで新しいプロパティの PROPERTYKEY 構造体を宣言できます。 次の例は、センサー、PROPERTYKEY の宣言\_読み取りプロパティ。 この例が表示されます、 *WpdObjectProperties.cpp*ファイル。

```cpp
DECLARE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

PROPERTYKEY を宣言するだけでなく、キーを定義する必要があります。 センサーの定義\_に読み取りキーが表示されます、 *Stdafx.h*ファイル。

```cpp
DEFINE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

*WpdObjectProperties.cpp*ファイルには PROPERTKEY 構造体の 3 つの配列の定義が含まれています。 これらのアレイは、サポートされている、関連するプロパティのコレクションを識別します。 1 つ目は、デバイスとセンサーの両方のオブジェクトに共通するプロパティを識別する PROPERTYKEYs の配列です。

```cpp
const PROPERTYKEY g_SupportedCommonProperties[] =
{
    WPD_OBJECT_ID,
    WPD_OBJECT_PERSISTENT_UNIQUE_ID,
    WPD_OBJECT_PARENT_ID,
    WPD_OBJECT_NAME,
    WPD_OBJECT_FORMAT,
    WPD_OBJECT_CONTENT_TYPE,
    WPD_OBJECT_CAN_DELETE,
};
```

使用する場合、 *WpdInfo.exe*デバイスとセンサーの現在のプロパティを取得するツールで、前の配列内のプロパティは、両方の一覧に表示します。

2 番目の配列は、デバイス オブジェクトをサポートするプロパティを識別する PROPERTYKEYS の配列です。

```cpp
const PROPERTYKEY g_SupportedDeviceProperties[] =
{
    WPD_DEVICE_FIRMWARE_VERSION,
    WPD_DEVICE_POWER_LEVEL,
    WPD_DEVICE_POWER_SOURCE,
    WPD_DEVICE_PROTOCOL,
    WPD_DEVICE_MODEL,
    WPD_DEVICE_SERIAL_NUMBER,
    WPD_DEVICE_SUPPORTS_NON_CONSUMABLE,
    WPD_DEVICE_MANUFACTURER,
    WPD_DEVICE_FRIENDLY_NAME,
    WPD_DEVICE_TYPE,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

この配列内のさまざまな静的プロパティに割り当てられている値で定義されます*WpdObjectProperties.h*します。

```cpp
#define DEVICE_PROTOCOL_VALUE            L"Sensor Protocol ver 1.00"
#define DEVICE_FIRMWARE_VERSION_VALUE    L"1.0.0.0"
#define DEVICE_POWER_LEVEL_VALUE         100
#define DEVICE_MODEL_VALUE               L"RS232 Sensor"
#define DEVICE_FRIENDLY_NAME_VALUE       L"Parallax BS2 Sensor"
#define DEVICE_MANUFACTURER_VALUE        L"Windows Portable Devices Group"
#define DEVICE_SERIAL_NUMBER_VALUE       L"01234567890123-45676890123456"
#define DEVICE_SUPPORTS_NONCONSUMABLE_VALUE    FALSE
```

これらの値が割り当てられている、 **WpdObjectProperties::GetPropertyValuesForObject**メソッド。

たとえば、このメソッドから抜粋がデバイス モデルの文字列 (視差 BS2 センサー) を割り当てます WPD に\_デバイス\_モデルのプロパティ。

```cpp
if (IsEqualPropertyKey(Key, WPD_DEVICE_MODEL))
{
    hr = pValues->SetStringValue(WPD_DEVICE_MODEL, DEVICE_MODEL_VALUE);
    CHECK_HR(hr, "Failed to set WPD_DEVICE_MODEL");
}
```

3 番目の配列には、一般的なオブジェクトのプロパティだけでなく、センサー オブジェクトをサポートするプロパティを識別する PROPERTYKEYS の配列です。

```cpp
const PROPERTYKEY g_SupportedSensorProperties[] =
{
    SENSOR_READING,
    SENSOR_UPDATE_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

これらの値が割り当てられて、 **WpdObjectProperties::GetPropertyValuesForObject**メソッド。 ただし、センサーに割り当てられている値\_読み取りとセンサー\_UPDATE\_間隔のプロパティが定数ではありません。 代わりに、2 つのヘルパー関数によってリアルタイムで取得される値は。**WpdObjectProperties::GetSensorReading**と**WpdObjectProperties::GetUpdateInterval**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)









