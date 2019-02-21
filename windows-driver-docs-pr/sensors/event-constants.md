---
title: イベント定数
description: センサー プラットフォームでは、ドライバーのイベントの次の定数を定義します。
ms.assetid: d9bcfda4-d731-462f-802d-99c85911a6ca
keywords:
- イベント定数
- センサー デバイス
topic_type:
- apiref
api_name:
- Event Constants
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b5ad2115639364fbec507f14ef94bb11ca4aa658
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537102"
---
# <a name="event-constants"></a>イベント定数


センサー プラットフォームでは、ドライバーのイベントの次の定数を定義します。

### <a name="sensor-event-types"></a>センサー イベントの種類

センサー プラットフォームでは、次のセンサー イベントの種類の識別子を定義します。

|名前|説明|
|--|--|
|SENSOR_EVENT_DATA_UPDATED|新しいデータが使用できることを示します。|
|SENSOR_EVENT_PROPERTY_CHANGED|プロパティ値が変更されたことを示します。|
|SENSOR_EVENT_STATE_CHANGED|たとえば、操作の状態の変更を SENSOR_STATE_READY SENSOR_STATE_INITIALIZING からを示します。|

 

### <a name="sensor-event-propertykeys"></a>センサー イベント PROPERTYKEYs

センサー プラットフォームは、次を定義します。 **PROPERTYKEY**センサー イベントのパラメーターを特定します。

|名前|説明|
|--|--|
|SENSOR_EVENT_PARAMETER_EVENT_ID|示します、 <strong>GUID</strong>値[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486) SENSOR_EVENT_DATA_UPDATED など、イベントの種類 ID です。|
|SENSOR_EVENT_PARAMETER_STATE|示しますの符号なし整数値[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486) SENSOR_STATE_READY など、センサーの状態です。 状態変更イベントを発生させるのには、呼び出す[ <strong>ISensorClassExtension::PostStateChange</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)します。 イベントを発生させる SENSOR_EVENT_PARAMETER_STATE を明示的に指定する必要はありません。|

 

<a name="requirements"></a>要件
------------

| | |
|--|--|
| サポートされている最小のクライアント | Windows 7 |
| サポートされている最小のサーバー | サポートなし |
| バージョン | Windows 7 で使用できます。|
| Header | Sensors.h |



## <a name="see-also"></a>関連項目


[センサー ドライバーのイベントについて](about-sensor-driver-events.md)

[データのフィルター処理](filtering-data.md)

[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)

[**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)

 

 






