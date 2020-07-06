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
ms.openlocfilehash: dc10d3f888c3b7dd4086377a07bbbbab7f8495af
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968125"
---
# <a name="event-constants"></a>イベント定数


センサープラットフォームは、ドライバーイベントの次の定数を定義します。

### <a name="sensor-event-types"></a>センサーイベントの種類

センサープラットフォームでは、次のセンサーイベントの種類の識別子が定義されています。

|名前|[説明]|
|--|--|
|SENSOR_EVENT_DATA_UPDATED|新しいデータが使用可能であることを示します。|
|SENSOR_EVENT_PROPERTY_CHANGED|プロパティ値が変更されたことを示します。|
|SENSOR_EVENT_STATE_CHANGED|SENSOR_STATE_INITIALIZING から SENSOR_STATE_READY へなど、操作状態が変更されたことを示します。|

 

### <a name="sensor-event-propertykeys"></a>センサーイベントの PROPERTYKEYs

センサーのプラットフォームでは、センサーイベントのパラメーターを識別するために、次の**Propertykey**が定義されています。

|名前|[説明]|
|--|--|
|SENSOR_EVENT_PARAMETER_EVENT_ID|[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)の<strong>GUID</strong>値が、SENSOR_EVENT_DATA_UPDATED などのイベントの種類の ID であることを示します。|
|SENSOR_EVENT_PARAMETER_STATE|[Iportabledevicevalues](https://go.microsoft.com/fwlink/p/?linkid=131486)の符号なし整数値がセンサーの状態 (SENSOR_STATE_READY など) であることを示します。 状態変更イベントを発生させるには、 [<strong>ISensorClassExtension::P oststatechange</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)を呼び出します。 SENSOR_EVENT_PARAMETER_STATE を明示的に指定しなくてもイベントを発生させることができます。|

 

<a name="requirements"></a>要件
------------

**サポートされている最低限のクライアント**: Windows 7

**サポートされている最小サーバー**: サポートされていません

**バージョン**: Windows 7 で利用可能

**ヘッダー**: センサー. h




## <a name="see-also"></a>関連項目


[センサー ドライバーのイベントについて](about-sensor-driver-events.md)

[データのフィルター処理](filtering-data.md)

[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)

[**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)

 

 






