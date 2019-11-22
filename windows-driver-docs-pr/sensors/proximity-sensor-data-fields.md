---
title: 近接センサー データ フィールド
description: このトピックでは、近接センサーに固有のデータフィールドについて説明します。
ms.assetid: 03B561DB-FAF2-4404-AA49-6A0DA139AA11
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e54cd2c045a773deb46a66133db61cc92e0e2f35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842334"
---
# <a name="proximity-sensor-data-fields"></a>近接センサー データ フィールド


このトピックでは、近接センサーに固有のデータフィールドについて説明します。

次の表は、データフィールドを示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_ProximityDetection|VT_BOOL|必須|オブジェクトがセンサーの近くにあることを示します。|
|PKEY_SensorData_ProximityDistanceMillimeters|VT_UI4|省略可能|検出されたオブジェクトへの距離 (ミリメートル単位)。|

 

## <a name="remarks"></a>注釈


センサーが**PKEY\_sensordata\_ProximityDistanceMillimeters**データフィールドをサポートしている場合、 **PKEY\_sensordata\_ProximityDistanceMillimeters** data フィールドの[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)からの呼び出しに応答して、センサーは次のデータフィールド*プロパティ*を報告する必要があります。

|データフィールドプロパティ|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorDataField_RangeMinimum|VT_R4 (float)|必須|センサーの有効な検出範囲 (ミリメートル単位) の下限 (両端を含む) を示します。|
|PKEY_SensorDataField_RangeMaximum|VT_R4 (float)|必須|センサーの有効な検出範囲 (ミリメートル単位) の上限 (両端を含む) を示します。|

 

>[!NOTE]
> 有効な検出範囲は、センサーからオブジェクトまでの直線距離です。 この距離は、センサーが指している軸に沿って測定され、実際の境界を含みます。

 

ドライバーがこれらのデータフィールドプロパティを報告できなかった場合でも、アプリは WinRT API を使用して近接センサーを検出できます。 ただし、これらのアプリはセンサーのサポート範囲を認識しないため、センサーを使用しないことを決定する場合があります。

## <a name="related-topics"></a>関連トピック


[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






