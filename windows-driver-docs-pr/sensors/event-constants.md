---
title: イベント定数
description: センサープラットフォームは、ドライバーイベントの次の定数を定義します。
ms.assetid: d9bcfda4-d731-462f-802d-99c85911a6ca
keywords:
- イベント定数
- センサーデバイス
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
ms.openlocfilehash: fc51c1a7933b4599cbcb388472efa60e653fd450
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841683"
---
# <a name="event-constants"></a>イベント定数


センサープラットフォームは、ドライバーイベントの次の定数を定義します。

### <a name="sensor-event-types"></a>センサーイベントの種類

センサープラットフォームでは、次のセンサーイベントの種類の識別子が定義されています。

|名前|説明|
|--|--|
|SENSOR_EVENT_DATA_UPDATED|新しいデータが使用可能であることを示します。|
|SENSOR_EVENT_PROPERTY_CHANGED|プロパティ値が変更されたことを示します。|
|SENSOR_EVENT_STATE_CHANGED|SENSOR_STATE_INITIALIZING から SENSOR_STATE_READY など、操作状態が変更されたことを示します。|

 

### <a name="sensor-event-propertykeys"></a>センサーイベントの PROPERTYKEYs

センサーのプラットフォームでは、センサーイベントのパラメーターを識別するために、次の**Propertykey**が定義されています。

|名前|説明|
|--|--|
|SENSOR_EVENT_PARAMETER_EVENT_ID|[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)の<strong>GUID</strong>値が、SENSOR_EVENT_DATA_UPDATED などのイベントの種類の ID であることを示します。|
|SENSOR_EVENT_PARAMETER_STATE|[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)の符号なし整数値がセンサーの状態 (SENSOR_STATE_READY など) であることを示します。 状態変更イベントを発生させるには、 [<strong>ISensorClassExtension::P oststatechange</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)を呼び出します。 SENSOR_EVENT_PARAMETER_STATE を明示的に指定しなくてもイベントを発生させることができます。|

 

<a name="requirements"></a>要件
------------

| | |
|--|--|
| サポートされている最小のクライアント | Windows 7 |
| サポートされている最小のサーバー | サポートなし |
| バージョン | Windows 7 で利用可能|
| Header | センサー. h |



## <a name="see-also"></a>関連項目


[センサードライバーのイベントについて](about-sensor-driver-events.md)

[データのフィルター処理](filtering-data.md)

[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)

[**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)

 

 






