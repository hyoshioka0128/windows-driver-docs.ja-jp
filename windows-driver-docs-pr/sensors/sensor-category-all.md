---
title: センサー\_カテゴリ\_すべて
description: センサー\_カテゴリ\_すべてのカテゴリは、すべてのセンサーのプラットフォームで定義されているカテゴリのセットを表します。
ms.assetid: 9a4524d2-055c-46e0-9650-66e6f2872fbc
keywords: SENSOR_CATEGORY_ALL センサー デバイス
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_ALL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2c4150aa1e8e6be42ce8d0cc6ffd2de7101e21f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384895"
---
# <a name="sensorcategoryall"></a>センサー\_カテゴリ\_すべて


センサー\_カテゴリ\_すべてのカテゴリは、すべてのセンサーのプラットフォームで定義されているカテゴリのセットを表します。

## <a name="platform-defined-property-keys"></a>プラットフォーム定義されているプロパティのキー

このカテゴリには、次のプラットフォームで定義されているデータ フィールドが含まれています。

|データの種類|種類|説明|
|--|--|--|
|SENSOR_DATA_TYPE_TIMESTAMP|VT_FILETIME|すべてのデータのレポートに必要です。 データ レポートが作成された時間と各データ レポートをマークします。 世界協定時刻 (UTC) を使用します。|
 

>[!IMPORTANT]
> 各プラットフォームで定義されている共通のデータ型**PROPERTYKEY**共通に基づいて**GUID**センサーという\_データ\_型\_共通\_GUID。 予約済みの基本値は、使用しないでくださいこの**GUID**プロパティ キーを定義します。

 

## <a name="requirements"></a>要件

| | |
|--|--|
|サポートされている最小のクライアント|Windows 7|
|サポートされている最小のサーバー|サポートなし|
|バージョン|Windows 7 で使用できます。|
|Header|Sensors.h|
 

 





