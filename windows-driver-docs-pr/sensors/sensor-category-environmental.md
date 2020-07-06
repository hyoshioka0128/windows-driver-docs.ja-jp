---
title: センサー \_ カテゴリの \_ 環境
description: センサーカテゴリの環境カテゴリには、 \_ \_ 周囲の環境または気象に関する情報を提供するセンサーが含まれています。
ms.assetid: 49839092-0792-4e89-bc3a-7defc4730937
keywords:
- SENSOR_CATEGORY_ENVIRONMENTAL センサーデバイス
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
ms.openlocfilehash: 868ede4c243b955b52a77737c66fa16d533168d1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968235"
---
# <a name="sensor_category_environmental"></a>センサー \_ カテゴリの \_ 環境


センサーカテゴリの環境カテゴリには、 \_ \_ 周囲の環境または気象に関する情報を提供するセンサーが含まれています。

### <a name="platform-defined-sensor-types"></a>プラットフォームで定義されたセンサーの種類

このカテゴリには、次のプラットフォームで定義されたセンサーの種類が含まれます。

|センサーの種類|説明|
|--|--|
|SENSOR_TYPE_ENVIRONMENTAL_ATMOSPHERIC_PRESSURE|Barometers.|
|SENSOR_TYPE_ENVIRONMENTAL_HUMIDITY|Hygrometers.|
|SENSOR_TYPE_ENVIRONMENTAL_TEMPERATURE|温度計.|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_DIRECTION|Weather vanes。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_SPEED|Anemometers。|

 

### <a name="platform-defined-data-fields"></a>プラットフォーム定義のデータフィールド

このカテゴリには、次のプラットフォーム定義のデータフィールドが含まれます。

|データの種類|Type|説明|
|--|--|--|
|SENSOR_DATA_TYPE_ATMOSPHERIC_PRESSURE_BAR|VT_R4|Atmospheres (バー) の大気圧。|
|SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS|VT_R4|気温 (摂氏)。|
|SENSOR_DATA_TYPE_RELATIVE_HUMIDITY_PERCENT|VT_R4|相対湿度 (パーセント)。|
|SENSOR_DATA_TYPE_WIND_DIRECTION_DEGREES_ANTICLOCKWISE|VT_R4|磁方位を基準とする風向 (度)。 北部は 0.0 (x 軸の上部) として表され、値は反時計回りの回転で増加します。 Z 軸は上向きの位置を示します。|
|SENSOR_DATA_TYPE_WIND_SPEED_METERS_PER_SECOND|VT_R4|1秒あたりのメートル単位の風速。|

 

>[!IMPORTANT]
> 各プラットフォーム定義の環境データ型**Propertykey**は、センサーデータ型の環境 GUID という名前の共通の**guid**に基づいてい \_ \_ \_ \_ ます。 予約済みの基本値であるため、この**GUID**を使用して独自のプロパティキーを定義しないでください。

 

## <a name="requirements"></a>要件


**サポートされている最低限のクライアント**: Windows 7

**サポートされている最小サーバー**: サポートされていません

**バージョン**: Windows 7 で使用できます。

**ヘッダー**: センサー. h



 

 





