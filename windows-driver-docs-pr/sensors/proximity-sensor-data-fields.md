---
title: 近接センサーのデータ フィールド
description: このトピックでは、近接センサーに固有のデータ フィールドに関する情報を提供します。
ms.assetid: 03B561DB-FAF2-4404-AA49-6A0DA139AA11
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e502155193fa29a7f1ff00d4c76110f81e10f727
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552922"
---
# <a name="proximity-sensor-data-fields"></a>近接センサーのデータ フィールド


このトピックでは、近接センサーに固有のデータ フィールドに関する情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)を参照してください。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_ProximityDetection|VT_BOOL|必須|オブジェクトが、センサーの近接度内にあることを示しています。|
|PKEY_SensorData_ProximityDistanceMillimeters|VT_UI4|省略可能|ミリメートル単位で、検出されたオブジェクト間の距離。|

 

## <a name="remarks"></a>注釈


センサーをサポートしている場合、**鍵\_SensorData\_ProximityDistanceMillimeters**からの呼び出しに応答しでのデータ フィールド[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)用、**鍵\_SensorData\_ProximityDistanceMillimeters**データ フィールドに、センサーは、次のデータ フィールドをレポートする必要があります*プロパティ*:

|データ フィールドのプロパティ|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorDataField_RangeMinimum|VT_R4 (float)|必須|(包括) ミリメートル単位のセンサーの検出が有効な範囲の下限の境界を示します。|
|PKEY_SensorDataField_RangeMaximum|VT_R4 (float)|必須|ミリメートル単位のセンサーの検出が有効な範囲の (包括) の上限の境界を示します。|

 

>[!NOTE]
> 検出の有効な範囲は、オブジェクトに、センサーからの直線距離です。 センサーをポイントすると、し、実際の境界を含めたが軸に沿った距離が測定されます。

 

ドライバーは、これらのデータ フィールドのプロパティをレポートに失敗した場合、アプリは WinRT API を使用して近接センサーを検出できます。 ただし、これらのアプリが、サポートされている範囲、センサーの登録されていないと、センサーを使用しないように指定します。

## <a name="related-topics"></a>関連トピック


[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






