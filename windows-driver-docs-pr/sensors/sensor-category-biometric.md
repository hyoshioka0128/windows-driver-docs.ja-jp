---
title: センサー \_ カテゴリの \_ 生体認証
description: センサー \_ カテゴリの \_ 生体認証カテゴリには、生きていることに関する情報を提供するセンサーが含まれています。
ms.assetid: e26073e1-11cc-40a9-9a60-3a15ceb46059
keywords:
- SENSOR_CATEGORY_BIOMETRIC センサーデバイス
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
ms.openlocfilehash: 6f59e3b3ea0939f75bac2850900f2daf2bbd8d6d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968447"
---
# <a name="sensor_category_biometric"></a>センサー \_ カテゴリの \_ 生体認証


センサー \_ カテゴリの \_ 生体認証カテゴリには、生きていることに関する情報を提供するセンサーが含まれています。

## <a name="platform-defined-sensor-types"></a>プラットフォームで定義されたセンサーの種類

このカテゴリには、次のプラットフォームで定義されたセンサーの種類が含まれます。

|センサーの種類|説明|
|--|--|
|SENSOR_TYPE_HUMAN_PRESENCE|人間の存在を検出するセンサー。|
|SENSOR_TYPE_HUMAN_PROXIMITY|人間の距離を検出するセンサー。|
|SENSOR_TYPE_TOUCH|タッチセンサー。|

 

### <a name="platform-defined-data-fields"></a>プラットフォーム定義のデータフィールド

このカテゴリには、次のプラットフォーム定義のデータフィールドが含まれます。

|データの種類|Type|説明|
|--|--|--|
|SENSOR_DATA_TYPE_HUMAN_PRESENCE|VT_BOOL|人間がコンピューターを使用しているときに VARIANT_TRUE します。|
|SENSOR_DATA_TYPE_HUMAN_PROXIMITY_METERS|VT_R4|人間とコンピューター間の距離 (メートル単位)。|
|SENSOR_DATA_TYPE_TOUCH_STATE|VT_BOOL|タッチセンサーにタッチしているときに VARIANT_TRUE します。それ以外の場合は VARIANT_FALSE ます。|

 

>[!IMPORTANT]
> 各プラットフォーム定義の生体認証データ型**Propertykey**は、センサー **GUID** \_ データ \_ 型 \_ 生体認証 Guid という名前の共通の GUID に基づいてい \_ ます。 予約済みの基本値であるため、この**GUID**を使用して独自のプロパティキーを定義しないでください。

 

## <a name="requirements"></a>要件


**サポートされている最低限のクライアント**: Windows 7

**サポートされている最小サーバー**: サポートされていません

**バージョン**: Windows 7 で使用できます。

**ヘッダー**: センサー. h


 

 





