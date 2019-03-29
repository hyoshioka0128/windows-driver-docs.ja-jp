---
title: センサー\_カテゴリ\_生体認証
description: センサー\_カテゴリ\_生体認証のカテゴリには、生物に関する情報を提供するセンサーが含まれています。
ms.assetid: e26073e1-11cc-40a9-9a60-3a15ceb46059
keywords:
- SENSOR_CATEGORY_BIOMETRIC センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_BIOMETRIC
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b76336448a5b6ef1a27e297f8548b0e7627747c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574801"
---
# <a name="sensorcategorybiometric"></a>センサー\_カテゴリ\_生体認証


センサー\_カテゴリ\_生体認証のカテゴリには、生物に関する情報を提供するセンサーが含まれています。

## <a name="platform-defined-sensor-types"></a>プラットフォーム定義されているセンサーの種類

このカテゴリには、次のプラットフォームで定義されているセンサーの種類が含まれています。

|センサーの種類|説明|
|--|--|
|SENSOR_TYPE_HUMAN_PRESENCE|人間の存在を検出するセンサー。|
|SENSOR_TYPE_HUMAN_PROXIMITY|人間の近接性を検出するセンサー。|
|SENSOR_TYPE_TOUCH|タッチ センサー。|

 

### <a name="platform-defined-data-fields"></a>プラットフォーム定義されているデータ フィールド

このカテゴリには、次のプラットフォームで定義されているデータ フィールドが含まれています。

|データ型|型|説明|
|--|--|--|
|SENSOR_DATA_TYPE_HUMAN_PRESENCE|VT_BOOL|人間がコンピューターを使用する場合は VARIANT_TRUE です。|
|SENSOR_DATA_TYPE_HUMAN_PROXIMITY_METERS|VT_R4|人間とメートル単位で、コンピューター間の距離。|
|SENSOR_DATA_TYPE_TOUCH_STATE|VT_BOOL|タッチ センサーが処理された場合は VARIANT_TRUE、場合は variant_false になります。|

 

>[!IMPORTANT]
> 生体認証データのプラットフォームで定義されている各種**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_型\_生体認証の\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

## <a name="requirements"></a>必要条件


| | |
|--|--|
|サポートされている最小のクライアント|Windows 7|
|サポートされている最小のサーバー|サポートなし|
|バージョン|Windows 7 で使用できます。|
|Header|Sensors.h|

 

 





