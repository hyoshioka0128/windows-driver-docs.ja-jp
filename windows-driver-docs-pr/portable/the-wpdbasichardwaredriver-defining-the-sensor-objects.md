---
Description: ソース オブジェクトの定義
title: ソース オブジェクトの定義
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 092e2a6207fee203b9af46854db5e3031ddc852d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378206"
---
# <a name="defining-the-sensor-objects"></a>ソース オブジェクトの定義


Windows ポータブル デバイス (WPD)、デバイス上の論理エンティティと呼びますオブジェクト。 オブジェクトは、デバイスの情報や機能の部分を表すことができます。 任意のオブジェクトには、1 つまたは複数のプロパティがあります。 プロパティは、オブジェクトの説明のメタデータとして考えることができます。 たとえば、サンプル気温・湿度センサーで TempHumidity オブジェクトがセンサーをサポート\_読み取りプロパティ。 このプロパティは、現在の温度と相対湿度デバイスの取得を指定します。

WpdHelloWorldDriver には、次の表に示すオブジェクトがサポートしています。

| オブジェクト  | 説明                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| デバイス  | 説明のプロパティを含むルート オブジェクト、ファームウェアのバージョン、モデル、およびフレンドリ名。 |
| ストレージ | たとえば、プロパティを公開するオブジェクトを記憶域容量、ファイル システムの種類では、および空きバイト数。         |
| Folder  | たとえば、フォルダー名のプロパティを公開するオブジェクト。                                                             |
| ファイル    | ファイル名と実際のファイルの内容などのプロパティを公開するオブジェクト。                                      |

 

記憶域、フォルダー、またはファイル オブジェクト サンプル センサーをサポートするため、WpdBasicHardwareDriver はこれらのオブジェクトを実装しません。 代わりに、各センサーの種類は、1 つのオブジェクトで表されます。 次の表では、WpdBasicHardwareDriver をサポートするオブジェクトが一覧表示します。

| オブジェクト       | 説明                                                                                                                                |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| デバイス       | 説明のプロパティを含むルート オブジェクト、ファームウェアのバージョン、モデル、およびフレンドリ名。                 |
| TempHumidity | 温度の読み取りと湿度を読むと、さらに編集可能な更新間隔プロパティを表示するための機能のオブジェクト。 |
| Compass      | 機能オブジェクトには、読み取り、編集可能な更新間隔プロパティおよびコンパスが表示されます。                          |
| PIR          | 読み取り、編集可能な更新間隔プロパティとパッシブの赤外線を表示するための機能のオブジェクト。                 |
| QTI          | 読み取り、編集可能な更新間隔プロパティと周辺光を表示するための機能のオブジェクト。                    |
| 柔軟な         | 読み取り、負荷を表示する機能のオブジェクトだけでなく編集可能な更新間隔プロパティ。                         |
| Ping         | 読み取り、距離を表示する機能のオブジェクトだけでなく編集可能な更新間隔プロパティ。                         |
| Piezo        | 読み取り、振動を表示する機能のオブジェクトだけでなく編集可能な更新間隔プロパティ。                        |
| Memsic       | 読み取り、加速度計 2 軸を表示する機能のオブジェクトだけでなく編集可能な更新間隔プロパティ。             |
| 日立      | 読み取り、3 軸加速度計を表示する機能のオブジェクトだけでなく編集可能な更新間隔プロパティ。             |

 

WPD、オブジェクトが文字列で識別されます。 デバイス オブジェクトの文字列識別子が定義されている、 *Portabledevice.h*ファイル。

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

センサー オブジェクトの文字列識別子が定義されている、 *WpdObjectProperties.h* WpdBasicHardwareDriver のファイル。

```cpp
#define SENSOR_OBJECT_ID             L"Sensor"
#define SENSOR_OBJECT_NAME_VALUE          L"Parallax Sensor"
#define COMPASS_SENSOR_OBJECT_ID              L"Compass"
#define COMPASS_SENSOR_OBJECT_NAME_VALUE      L"HM55B Compass Sensor"
#define PIR_SENSOR_OBJECT_ID                  L"PIR"
#define PIR_SENSOR_OBJECT_NAME_VALUE          L"Passive Infra-Red Sensor"
#define QTI_SENSOR_OBJECT_ID                  L"QTI"
#define QTI_SENSOR_OBJECT_NAME_VALUE          L"QTI Light Sensor"
#define FLEX_SENSOR_OBJECT_ID                 L"Flex"
#define FLEX_SENSOR_OBJECT_NAME_VALUE         L"Flex Force Sensor"
#define PING_SENSOR_OBJECT_ID                 L"Ping"
#define PING_SENSOR_OBJECT_NAME_VALUE         L"Ultrasonic Distance Sensor"
#define PIEZO_SENSOR_OBJECT_ID                L"Piezo"
#define PIEZO_SENSOR_OBJECT_NAME_VALUE        L"Piezo Vibration Sensor"
#define TEMP_SENSOR_OBJECT_ID                 L"TempHumidity"
#define TEMP_SENSOR_OBJECT_NAME_VALUE         L"Sensiron Temperature and Humidity Sensor"
#define MEMSIC_SENSOR_OBJECT_ID               L"Memsic"
#define MEMSIC_SENSOR_OBJECT_NAME_VALUE       L"Memsic Dual-Axis G-Force Sensor"
#define HITACHI_SENSOR_OBJECT_ID              L"Hitachi"
#define HITACHI_SENSOR_OBJECT_NAME_VALUE      L"Hitachi Tri-Axis G-Force Sensor"
```

これらのオブジェクト識別子の定数は、オブジェクトの列挙を処理するソース モジュール内でメソッドに渡される (*WpdObjectEnum.cpp*)、プロパティの処理 (*WpdObjectProperties.cpp*)、およびデバイスの機能の取得 (*WpdCapabilities.cpp*)。 次の抜粋、 **WpdObjectEnumerator::OnFindNext**メソッドは、サンプル ドライバーのこれらの識別子がオブジェクトの列挙体で使用する方法を示しています。

```cpp
// If the enumeration context reports that there are more objects to return, then continue, if not,
    // return an empty results set.
    if ((hr == S_OK) && (pEnumeratorContext != NULL) && (pEnumeratorContext->HasMoreChildrenToEnumerate() == TRUE))
    {
        if (pEnumeratorContext->m_strParentObjectID.CompareNoCase(L"") == 0)
        {
            // We are being asked for the WPD_DEVICE_OBJECT_ID
            hr = AddStringValueToPropVariantCollection(pObjectIDCollection, WPD_DEVICE_OBJECT_ID);
            CHECK_HR(hr, "Failed to add 'DEVICE' object ID to enumeration collection");

            // Update the number of children we are returning for this enumeration call
            NumObjectsEnumerated++;
        }
        else if (pEnumeratorContext->m_strParentObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
        {
    
            // We are being asked for direct children of the WPD_DEVICE_OBJECT_ID
            switch (m_pBaseDriver->m_SensorType)
            {
            case WpdBaseDriver::UNKNOWN:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::COMPASS:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, COMPASS_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::SENSIRON:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, TEMP_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::FLEX:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, FLEX_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PING:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PING_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PIR:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PIR_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::MEMSIC:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, MEMSIC_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::QTI:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, QTI_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PIEZO:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PIEZO_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::HITACHI:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, HITACHI_SENSOR_OBJECT_ID);
                    break;
                default:
                    break;
```

WpdBasicHardwareDriver サンプルでは、ドライバーは、すべてのセンサーを含む 1 つの機能カテゴリを定義します。 ドライバー開発者はこのサンプルを拡張し、アプリケーションがどのセンサーを識別できるように、各センサーの種類に個別の機能カテゴリを定義、ドライバーがサポートされます。 これは、開発者は、これらの新しいカテゴリが正しく返されるように WpdCapabilities::OnGetFunctionalCategories メソッドを変更が必要です。

 

 




