---
title: マーシャリング ヘルパーの関数
description: このトピックでは、sensorsutils ヘッダーファイル内のマーシャリングヘルパー関数について説明します。
ms.assetid: AE5C70E4-1971-4BAF-AE7D-315A15F030DD
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3719233c806d0f5d81d639e90235bd96d30a82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842448"
---
# <a name="marshalling-helper-functions"></a>マーシャリング ヘルパーの関数


このトピックでは、 *sensorsutils*ヘッダーファイル内のマーシャリングヘルパー関数について説明します。

これらのヘルパー関数は、v2 センサードライバーによって使用され、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

独自のマーシャリングヘルパー関数を実装する場合は、[**センサー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)構造体で列挙リストを設定するとき、または[**SensorsCxSensorDataReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)関数を使用して更新されたデータを報告するときに、ヘルパー関数を使用しないようにする必要があることに注意してください。

## <a name="in-this-section"></a>このセクションの内容


|トピック|説明|
|--|--|
|[タイムスタンプヘルパー](timestamp-helper.md)|タイムスタンプヘルパー関数は、v2 センサードライバーによって使用され、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) で使用されます。|
|[PropVariant ヘルパー](propvariant-helpers.md)|PropVariant ヘルパー関数は、センサーに関連付けられている[propvariant](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)構造を操作するために v2 センサードライバーによって使用されます。|
|[コレクションリストヘルパー](collection-list-helpers.md)|コレクションリストヘルパー関数は、 [SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体を操作するために、v2 センサードライバーによって使用されます。|
|[コレクションリストのシリアル化ヘルパー](collection-list-serialization-helpers.md)|コレクションリストのシリアル化ヘルパー関数は、v2 センサードライバーによって使用され、 [SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造に対するシリアル化関連の操作を実行します。|
|[コレクションリストレガシヘルパー](collection-list-legacy-helpers.md)|コレクションリストレガシヘルパー関数は、v2 センサードライバーが[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体と対話するために使用します。|

 

## <a name="requirements"></a>要件


**ヘッダー:** Sensorsutils

 

 





