---
title: センサー \_ カテゴリ \_ すべて
description: センサー \_ カテゴリ [ \_ すべて] カテゴリは、プラットフォームで定義されたすべてのセンサーカテゴリのセットを表します。
ms.assetid: 9a4524d2-055c-46e0-9650-66e6f2872fbc
keywords: SENSOR_CATEGORY_ALL センサーデバイス
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
ms.openlocfilehash: 0ea9aea5e7694a99724060c031e929088896a762
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968469"
---
# <a name="sensor_category_all"></a>センサー \_ カテゴリ \_ すべて


センサー \_ カテゴリ [ \_ すべて] カテゴリは、プラットフォームで定義されたすべてのセンサーカテゴリのセットを表します。

## <a name="platform-defined-property-keys"></a>プラットフォームで定義されたプロパティキー

このカテゴリには、次のプラットフォーム定義のデータフィールドが含まれます。

|データの種類|Type|説明|
|--|--|--|
|SENSOR_DATA_TYPE_TIMESTAMP|VT_FILETIME|すべてのデータレポートに必要です。 データレポートが作成された時刻で各データレポートをマークします。 世界協定時刻 (UTC) を使用します。|
 

>[!IMPORTANT]
> 各プラットフォーム定義の共通データ型**Propertykey**は、センサー **GUID** \_ データ型共通 guid という名前の共通 guid に基づいてい \_ \_ \_ ます。 予約済みの基本値であるため、この**GUID**を使用して独自のプロパティキーを定義しないでください。

 

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 7

**サポートされている最小サーバー**: サポートされていません

**バージョン**: Windows 7 で使用できます。

**ヘッダー**: センサー. h

 

 





