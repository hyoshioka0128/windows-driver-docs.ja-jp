---
title: センサー\_カテゴリ\_環境
description: センサー\_カテゴリ\_環境のカテゴリには、周囲の環境または天気に関する情報を提供するセンサーが含まれています。
ms.assetid: 49839092-0792-4e89-bc3a-7defc4730937
keywords:
- SENSOR_CATEGORY_ENVIRONMENTAL センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_ENVIRONMENTAL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d130f2a0e6a8667a0da6737742b5afc9700ee13d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527957"
---
# <a name="sensorcategoryenvironmental"></a>センサー\_カテゴリ\_環境


センサー\_カテゴリ\_環境のカテゴリには、周囲の環境または天気に関する情報を提供するセンサーが含まれています。

### <a name="platform-defined-sensor-types"></a>プラットフォーム定義されているセンサーの種類

このカテゴリには、次のプラットフォームで定義されているセンサーの種類が含まれています。

|センサーの種類|意味|
|--|--|
|SENSOR_TYPE_ENVIRONMENTAL_ATMOSPHERIC_PRESSURE|Barometers します。|
|SENSOR_TYPE_ENVIRONMENTAL_HUMIDITY|Hygrometers します。|
|SENSOR_TYPE_ENVIRONMENTAL_TEMPERATURE|温度計です。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_DIRECTION|風見します。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_SPEED|Anemometers します。|

 

### <a name="platform-defined-data-fields"></a>プラットフォーム定義されているデータ フィールド

このカテゴリには、次のプラットフォームで定義されているデータ フィールドが含まれています。

|データの種類|種類|意味|
|--|--|--|
|SENSOR_DATA_TYPE_ATMOSPHERIC_PRESSURE_BAR|VT_R4|大気圧の単位は気圧 (棒)。|
|SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS|VT_R4|温度を摂氏でします。|
|SENSOR_DATA_TYPE_RELATIVE_HUMIDITY_PERCENT|VT_R4|パーセンテージとして相対湿度。|
|SENSOR_DATA_TYPE_WIND_DIRECTION_DEGREES_ANTICLOCKWISE|VT_R4|方位は磁北、相対方向を風力 (度単位)。 North は、大きくと、左回りに回転値 0.0 (x 軸の上) として表されます。 Z 軸ポイント増加します。|
|SENSOR_DATA_TYPE_WIND_SPEED_METERS_PER_SECOND|VT_R4|1 秒あたりのメートル単位で風速。|

 

>[!IMPORTANT]
> 各プラットフォームで定義されている環境のデータ型**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_型\_環境\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

## <a name="requirements"></a>要件


| | |
|--|--|
|サポートされている最小のクライアント|Windows 7|
|サポートされている最小のサーバー|サポートなし|
|バージョン|Windows 7 で使用できます。|
|Header|Sensors.h|


 

 





