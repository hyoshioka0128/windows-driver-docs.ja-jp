---
title: センサーの構造
description: センサーの構造
ms.assetid: 94194998-8A56-48D3-9053-007526BF0ED2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78ff6b52c5dc652c99caa3b0a2b671c6614cae26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845489"
---
# <a name="sensor-structures"></a>センサーの構造

このセクションでは、センサーのさまざまなプロパティと機能へのアクセスを提供するセンサー構造について説明します。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|---|---|
|[SENSOR_VALUE_PAIR](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)|この構造体は、センサーのプロパティセクションに一覧表示されているプロパティキーと各キーが表すデータを組み合わせたものです。|
|[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)|この構造体には、各センサーのすべての SENSOR_VALUE_PAIR 構造体の一覧が含まれています。|
|[SENSOR_PROPERTY_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_property_list)|この構造体には、各センサーのすべての SENSOR_VALUE_PAIR 構造体の一覧が含まれています。|
|[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)|この構造体には、センサードライバーが各センサーのクラス拡張に渡す情報が含まれています。|
|[SENSOR_CONTROLLER_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)|この構造体には、ドライバーによって実装される必要があり、を呼び出すクラス拡張に渡されるコールバック関数へのポインターが含まれています。|
|SENSOR_DATA|この構造体は、センサー固有のデータ型を定義するために他のセンサーが使用する基本型を定義します。|
|SENSOR_DEVICE_CAPS|この構造体には、センサーコンポーネントの機能が記述されています。|
|SENSOR_DATA_HEADER|この構造体には、センサーの読み取りに関する情報が含まれます。|
|VEC3D|この構造体は、3D 配置データ用の1つのデータポイントを保持します。|
|四元数|この構造体は、単純な3-d 回転演算に使用される4次元ベクトルを表すために使用されます。|
|MATRIX3X3|この構造体は、一般的な 3 x の行列を表すために使用されます。|






